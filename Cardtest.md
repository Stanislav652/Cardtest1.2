# Проверка работоспособности программы IntelliJ IDEA в части функционирования валидации номера банковской карты #

1. Открыть программу IntelliJ IDEA
2. Нажать на клавишу New Project
3. На панели проекта раскрыть структуру каталогов и на каталоге src щёлкнуть правой кнопкой мыши и выбрать "New" -> "Java Class"
4. В открывшемся окне ввести "Main" и нажать клавишу "Enter"
5. Заменить содержимое открывшегося файла кодом:
 ```public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```
6. Нажать на зелёную стрелку на первой строке и выбрать "Run 'Main.main()'"
7. Заменить номер в коде на номер из списка ниже в строке "String number = "5351719427810741"
8. Нажать на зелёную стрелку на первой строке и выбрать "Run 'Main.main()'"
9. Номера валидных карт для проверки работоспособности программы:
* 4791781952880086
* 36099045475886
* 4485822270848
* 378954074728025
* 56236227162582715
* 501474315882629626
* 3537550599297173547
10. Номера невалидных карт для проверки работоспособности программы:
* 4523478956321568
* 2356879651235
* 36845123698532
* 789612758436159
* 3089451491346597
* 552648249135716348
* 4536871935716289143

Ожидаемый результат для проверки валидных номеров карт: Result is OK.

Ожидаемый результат для проверки невалидных номеров карт: Result is FAIL.