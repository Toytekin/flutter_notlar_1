## MİXİN kullanımı

## NEDİR ?
==> Flutter'da mixin, bir sınıfın davranışını başka bir sınıfa eklemek için kullanılan bir yapıdır. 

## Ne için kullanılır ?
==> Mixin, bir sınıfın özelliklerini diğer sınıflara kalıtım yoluyla aktarmak yerine, kod tekrarını önlemek için kullanılır.

## Nasıl kullanılırı ?
Mixin, with anahtar kelimesi kullanılarak bir sınıfa eklenir ve bir veya daha fazla mixin sınıfı kullanılabilir. Mixin sınıflarında sadece metotlar ve özellikler tanımlanır, ancak bu sınıfların kendilerine özgü bir durumları veya yapıcıları yoktur.

## Örenek-1
Örnek olarak, bir "LogMixin" sınıfı oluşturabiliriz ve bu sınıfın içinde loglama işlemleri gerçekleştiririz. Daha sonra bu mixin'i, loglama işlevselliğini eklemek istediğimiz diğer sınıflara ekleyebiliriz. Aşağıdaki örnek, "MyClass" sınıfına "LogMixin" sınıfını ekler:

##
class LogMixin {
  void log(String message) {
    print('[LOG] $message');
  }
}

class MyClass with LogMixin {
  void doSomething() {
    log('doing something');
  }
}
##

==> Bu örnekte, "LogMixin" sınıfı, "MyClass" sınıfına eklenmiştir. "MyClass" sınıfındaki "doSomething" metodu içinde "log" metodu kullanılabilir ve bu sayede loglama işlemleri yapılabilir.

!!! Uyarı!!!
Mixin yapısı, kod tekrarını önlemek ve sınıfları daha esnek hale getirmek için kullanışlı bir yapıdır. Ancak, doğru kullanılmadığında ve çok fazla mixin kullanıldığında karmaşık bir kod tabanına neden olabilir, bu nedenle mixin kullanımında dikkatli olunması önemlidir.


## Örenek-2
import 'package:flutter/material.dart';

mixin ArkaPlanRenkMixin {
  Color _backgroundColor = Colors.white;

  void setBackgroundColor(Color color) {
    _backgroundColor = color;
  }

  Color getBackgroundColor() {
    return _backgroundColor;
  }
}

// arkaplan ayarlamak için kullanılacak bir mixin
// setBackgrounColor ile mixin içindeki _backgroundColur değişkenimizi güncelliyoruz
// getBackgroundColor ile mixin içindeki _backgroundColur değikenimizi döndürüyoruz

==> Kullanımı
Container
  color:getBackgroundColor() //Containera renk ataması

ElevetadButton
  onpress
       setBackgroundColor(Colors.red); // Renk ayarlamsı
##

## Örenek-3
mixin Character {
  String name = '';
  int level = 0;

  int healthPoints = 0;
  int attackPoints = 0;

  void attack(Character opponent) {
    print(
        "$name is attacking ${opponent.name} with ${attackPoints} attack points!");
    opponent.healthPoints -= attackPoints;
    print(
        "${opponent.name}'s health points decreased to ${opponent.healthPoints}!");
  }
}

// Karakter sınıfları
class Warrior with Character {
  @override
  String name = 'deneme';

  @override
  int get level => 12;

  @override
  int get healthPoints => 150;

  @override
  int get attackPoints => 200;
}

class Mage with Character {
  @override
  String name = 'Mage';
  @override
  int level = 1;
  @override
  int healthPoints = 70;
  @override
  int attackPoints = 15;
}

class Archer with Character {
  @override
  String name = 'Archer';
  @override
  int level = 1;
  @override
  int healthPoints = 80;
  @override
  int attackPoints = 12;
}

void main() {
  Warrior warrior = Warrior();
  Mage mage = Mage();
  Archer archer = Archer();

  print("The battle begins!");
  warrior.attack(mage);
  mage.attack(warrior);
  archer.attack(mage);
  warrior.attack(archer);
}

##

