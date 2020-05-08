# Отчет о тестировании Credit Card Number Validator
## Краткое описание
09.05.2020  было проведено функциональное тестирование, тестирование методом граничных значений приложения Credit Card Number Validator.

На тестирование затрачен 1 час.

В результате тестирования выявлены следующие дефекты:

- [Не валидирует карты с 15-ти, 18-ти, 19-тизначными номерами](https://github.com/nastiamikh/Card-Number-Validator/issues/1)

# Описание процесса тестирования

В качестве тестовых данных использовались: 

- [Валидные номера карт с основными платежными системами - Visa, Master Card, Maestro, American Express](https://www.freeformatter.com/credit-card-number-generator-validator.html)
- [Валидные номера карт с платежной системой МИР](https://pay.alfabank.ru/ecommerce/instructions/merchantManual/pages/index/test_cards.html)
- Исходный код валидатора:
```java
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "";
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
Ожидаемый результат: валидатор выдает результат ```Result is FAIL``` на невалидные номера карт и результат ```Result is OK``` на валидные номера карт.

# Тестирование производилось в следующем окружении:

- операционная система Windows 10, версия 1809, разрядность 64x 
- версия Java 11.0.7