# flutter-study
//Dart의 reduce() 함수는 리스트와 같은 Iterable 객체에서 사용되며, 리스트의 요소들을 차례대로 합성
//이 함수는 리스트의 첫 번째와 두 번째 요소로 호출되고, 그 결과를 세 번째 요소와 다시 호출하는 방식
//Dart의 fold() 함수는 reduce()와 유사하게 리스트와 같은 Iterable 객체에서 사용되며, Iterable의 요소들을 하나의 값으로 줄이는 데 사용
//초기값 설정이 가능
//Dart에서 enum(열거형)은 관련된 상수들의 집합을 정의할 때 사용됩니다. 각 열거형은 열거된 값들로 구성되며, 이 값들은 특정 데이터 타입을 가지지 않는 상수로서 취급


// 상속 클래스
class Idol{
  final String name;
  final int membersCount;

//생성자
  Idol(this.name, this.membersCount);

  void sayName(){
    print('im ${this.name}.');
  }

  void sayMemberscount(){
    print('${this.name} memebers No. ${this.membersCount} .');
  }
}

//인터페이스
 class GirlGroup implements Idol{
  final String name;
  final int membersCount;

  GirlGroup(
      this.name,
      this.membersCount,
      );
  void sayName(){
    print('Im girl ${this.name}');
  }

  void sayMemberscount(){
    print('${this.name} members No. ${this.membersCount}.');
  }
}

//상속
class BoyGroup extends Idol{
  BoyGroup(
      String name,
      int membersCount,
      ) : super(
    name,
    membersCount,
  );
}

//믹스인
//클래스의 일부 기능을 다른 클래스에 재사용할 수 있도록 하는 방법
//다중 상속을 대신하는 개념으로, Dart에서는 extends 키워드로 단일 상속을 하면서 with 키워드로 여러 mixin을 적용
mixin IdolSingMixin on Idol{
  void sing(){
    print('${this.name} singing');
  }
}

class BoyGroup2 extends Idol with IdolSingMixin{
  BoyGroup2(super.name,
      super.membersCount,);

  void sayMale(){
    print('im boy.');
  }
}

void main() {
  BoyGroup bts = BoyGroup('BTS', 7);

  bts.sayMemberscount();
  bts.sayName();

  BoyGroup2 tmt = BoyGroup2('TMT', 8);
  tmt.sing();
  GirlGroup blackpink = GirlGroup('blping', 4)
  ..sayName()
  ..sayMemberscount();
  //캐스케이드 연산자 - 해당 인스턴스의 속성이나 멤버 함수를 사용
  
  blackpink.sayName();
  blackpink.sayMemberscount();

  final cache = Cache<List<int>>(
    data:[1,2,3],
  );

  print(cache.data.reduce((val, ele)=> val +ele));
}
//제네릭
// 데이터 타입을 일반화하여 여러 타입에 대해 동작
class Cache<T>{
  final T data;
  Cache({
    required this.data,

});
}
/****************************************************************************/

import 'dart:async';

// void main(){
//   addNumbers(1,1);
//   //delayed
//   addNumasync(2,2);
//   //async
// }
// 1 + 1 start!
// 1 + 1 code end
// 2 + 2 start!   딜레이 되는 와중에 대기 없이 다음코드 실행
// 1 + 1 = 2   3초 딜레이 후 코드 실행
// 2 + 2 = 4   awiat 가 잇으므로 3초 기다림
// 2 + 2 code end  await 대기 이후 실행

// 메인이 async 이므로 async 걸림 함수만 실행 가능
//차례대로 실행
//결괏값 반환
void main() async {
final result = await addNumasync(1,1);
print('result: $result');
final result2 = await addNumasync(2,2);
print('result2: $result2');

//stream - 비동기 이벤트 또는 데이터 시퀀스를 처리하는 데 사용되는 클래스
//일반적으로 파일 읽기, 네트워크 요청, 사용자 입력 처리 등에서 사용
final controller = StreamController();
final stream = controller.stream;



// final streamListener1 = stream.listen((val){
//   print(val);
// });
// controller.sink.add(1);
// controller.sink.add(1);
// controller.sink.add(3);
// controller.sink.add(4);
// controller.close();

final broadStream = controller.stream.asBroadcastStream();
final streamListener2 = broadStream.listen((val){
print('listening 1');
print(val);
});

final streamListener3 = broadStream.listen((val){
print('listening 2');
print(val);
});

controller.sink.add(1);
controller.sink.add(1);
controller.sink.add(3);
controller.sink.add(4);
controller.close();

playStream();
}

void addNumbers(int number1, int number2) {
print('$number1 + $number2 start!');

//딜레이 되는 중에 다음 코드가 실행 되므로 코드 끝이 먼저 나오고 과정이 나중에 나옴
Future.delayed(Duration(seconds: 3), () {
print('$number1 + $number2 = ${number1 + number2}');
});

print('$number1 + $number2 code end');


}

Future<int> addNumasync(int number1, int number2) async{
print('$number1 + $number2 start!');

await Future.delayed(Duration(seconds:3), (){
print('$number1 + $number2 = ${number1 + number2}');
});
print('$number1 + $number2 code end');

return number1 + number2;
}

//Stream 반환 함수는 async* 로 함수를 선언하고 yield 키워드로 반환
Stream<String> calculate(int number) async*{
for(int i = 0; i < 5; i++){
yield 'i = $i';
await Future.delayed(Duration(seconds:1));
}

}

playStream(){
calculate(1).listen((val){
print(val);
});
}