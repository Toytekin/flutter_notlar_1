## ENUM yapısı vekullanımı

enum Renkler { KIRMIZI, MAVI, YESIL, LACIVERT }

==> Burada Renkler adında bir enum oluşturduk
        + Enumlar String ifadeler ile yazılan işlerimizi kolaylaştıran yapılardır.

## renkleriGetir
Color renkleriGetir(Renkler renk) {
  switch (renk) {
    case Renkler.KIRMIZI:
      {
        return Colors.red;
      }
        .
        .
        .       
    default:
      return Colors.grey;
  }
}
##
==> Burada renkleriGetir adlı bir metot yazdık. Ve bu metot içerisine Renkler enumundan bir renk alıyor

## switc/case ler ile enum değerine göre istediğimiz rengi döndürüyoruz...

##  EXTENSİON KULLANIMI
        ==> BİR SINIFA FARKLI BİR ÖZELLİK KAZANDIRMAK İÇİN KULLANILIR

Flutter'da extension'lar, mevcut bir sınıfı genişletmek veya yeni fonksiyonellikler eklemek için kullanılan bir özelliktir. Extension'lar, dilde tanımlı olan bir sınıfın içinde bulunmayan fonksiyonların eklenmesine olanak tanır.

## StringExtensinKullanimi
extension StringExtensinKullanimi on String {
  String get kareAl {
    switch (this) {
      case 'iki':
        return (2 * 2).toString();
      case 'üç':
        return (3 * 3).toString();
      case 'dört':
        return (4 * 4).toString();
      case 'beş':
        return (5 * 5).toString();
      default:
        return 0.toString();
    }
  }
}
##
==> BuradaString sınıfımıza bir özellik ekledik.
        dedik ki string olarak iki,üç,dört yazılıp nokta ile kareAl çalıştırılırsa istediğim
        yukarıdaki işlemleri yap.

##  Text('beş'.kareAl)     ==>Burada 25 çıktısını alırız.

extension'lar ile var olan sınıflarımıza farklı özellikler kazandırarak efektif kullanabiliriz.

## Örnek 2


extension ListExtension<T> on List<T> {
  List<T> filter(bool Function(T) test) {
    List<T> result = [];
    for (T item in this) {
      if (test(item)) {
        result.add(item);
      }
    }
    return result;
  }
}

void main() {
  List<int> numbers = [1, 2, 3, 4, 5];
  List<int> evenNumbers = numbers.filter((number) => number.isEven);
  print(evenNumbers); // [2, 4]
}


Burada List sınıfımıza bir özelllik kazandırdık.
Kendisine gelen listeyi filter fonksiyonundan geçirerek çif mi tek mi onu ayırt eden bir 
fonksiyon.

bir liste oluşturuklen nokta ile bu fonksiyonumuzu çağırdık
##

## ENUM VE EXTENSİON 'un BİR ARADA KULLANIMI


enum TabItem {
  home,
  search,
  favorites,
  profile
}

extension TabItemExtension on TabItem { //TabItem'a bir özewllik kazandirıyoruz
  String get title {
    switch (this) {
      case TabItem.home://unumu çağırıyoruz
        return 'Home';  // Strin döndürüyoruz
      case TabItem.search:
        return 'Search';
      case TabItem.favorites:
        return 'Favorites';
      case TabItem.profile:
        return 'Profile';
      default:
        return '';
    }
  }
}

******
   bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentTab.index,
        onTap: _onTabTapped,
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: TabItem.home.title,// String çekme işlemi
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.search),
            label: TabItem.search.title,
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.favorite),
            label: TabItem.favorites.title,
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: TabItem.profile.title,
          ),
        ],
      ),
    );
  }

  Widget _buildPageForTab(TabItem tabItem) {
    switch (tabItem) {
      case TabItem.home:
        return HomeTab();
      case TabItem.search:
        return SearchTab();
      case TabItem.favorites:
        return FavoritesTab();
      case TabItem.profile:
        return ProfileTab();
      default:
        return SizedBox.shrink();
    }
  }
}


