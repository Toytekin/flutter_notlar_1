# Adım 1 == Model sınıfımızı oluşturalım
==> Gelen dataya göre bir model sınıfı oluşturmalısın
==> Bunun için yardımcı siteler zaten var

# Adım 2 == Servis dosyasını hazırlama

##
abstract class IReqresServices {
  IReqresServices(this.dio);
  final Dio dio;

  Future<DioApiModel?> fetchReqresitems();  //DioApiModel oluşturulan model sınıfı oluyor
}

##

## burada servis dosylarımızı hazırlıyoruz

class RecresServices extends IReqresServices {
  RecresServices(super.dio);

  @override
  Future<DioApiModel?> fetchReqresitems() async {
    final responese = await dio.get('https://reqres.in/api/users?page=2'); // Api adresi

    if (responese.statusCode != 404) {
      final jsonData = responese.data;
      var model = DioApiModel.fromMap(jsonData);
      return model;
    }
    return null;
  }
}
##

# ADım 3 == View Model sınıfı

==> view model sayesinde ekrana çzim ve dekor işlemleri dışında servis kodları vs başka bir dosyada tutuyoruz

##
abstract class ReqresViewModel extends State<ReqresView> with ProjeMixin {
  late final IReqresServices reqservices;  // servis
  List<Datum> listem = [];   // Gelen listem
  
  @override
  void initState() {
    super.initState();
    reqservices = RecresServices(services);
    fetch();
  }

  Future<void> fetch() async {
    listem = (await reqservices.fetchReqresitems())?.data ?? [];
    setState(() {});
  }
}

class ProjeMixin {
  final services =
      Dio(BaseOptions(baseUrl: 'https://reqres.in/api/users?page=2')); // link
}
##
==> Uyarı
        + abstract class oluşturuyoruz
        + sayfayı çizdiğimiz statfull veya statless dan <<extends State<ReqresView> >> kısmını alıp oluşturduğumuz bu sınıfa  exdents ediyoruz
        + Böylelikle buradaki kodlarımız statfull veya statless ile konuşabilecek

# Adım 4 == View dosyası


##
class ReqresView extends StatefulWidget {
  const ReqresView({super.key});

  @override
  State<ReqresView> createState() => _ReqresViewState();
}

class _ReqresViewState extends ReqresViewModel { // VİEW_MODEL İLE KONUŞABİLMESİ İÇİN  <<extends State<ReqresView> SİLİP BUNU YAZIYORUZ
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(),
        body: ListView.builder(
          itemCount: listem.length, //DİREK VİEW_MODEL İÇİNDEKİ LİSTEMİZİ ÇEKİYORUZ
          itemBuilder: (context, index) {
            return Card(
              child: ListTile(
                leading: CircleAvatar(
                    backgroundImage: NetworkImage(listem[index].avatar)),
                title: Text(listem[index].email),
                subtitle: Text(listem[index].firstName),
              ),
            );
          },
        ));
  }
}


##