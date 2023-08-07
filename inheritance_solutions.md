# Наследование

## Задача 1

  ```python
  class HeavenlyBody:
      'Родительский класс Planet'
  
      def __init__(self, name, age, temperature, radius):
          self.name = name
          self.age = age
          self.temperature = temperature
          self.radius = radius
  
      def display(self):
          print(f'Название: {self.name}')
          print(f'Возраст: {self.age} (млн. лет)')
          print(f'Температура: {self.temperature} (С)')
          print(f'Радиус: {self.radius} (км)')
  
  class Planet(HeavenlyBody):
      'Дочерний класс Planet'
  
      def __init__(self, name, age, temperature, radius, orbital_speed):
          super().__init__(name, age, temperature, radius)
          self.orbital_speed = orbital_speed
  
      def display(self):
          super().display()
          print(f'Орбитальная скорость: {self.orbital_speed} (км/с) \n')
  
  class Star(HeavenlyBody):
      'Дочерний класс Star'
  
      def __init__(self, name, age, temperature, radius, constellation):
          super().__init__(name, age, temperature, radius)
          self.constellation = constellation
  
      def display(self):
          super().display()
          print(f'Созвездие: {self.constellation} \n')
  ```


## Задача 2

   ```python
    import datetime
    
    class Pastry:
        def __init__(self, name, price, manufacture_date, term):
            self.id = id(self)
            self.name = name
            self.price = price
            self.manufacture_date = manufacture_date
            self.term = term
    
        def display(self):
            print(f'Название: {self.name}')
            print(f'Цена: {self.price} (руб.)')
            print(f'Дата изготовления: {self.manufacture_date}')
    
        def valid_until(self):
            today = datetime.date.today()
            end_date = self.manufacture_date + datetime.timedelta(days=self.term)
            remaining_time = end_date - today
            if remaining_time.days < 0:
                return 'Срок годности истек'
            else:
                return 'Срок годности истекает через {} дня'.format(remaining_time.days)
    
    class Cake(Pastry):
        def __init__(self, name, price, manufacture_date, term, filling):
            super().__init__(name, price, manufacture_date, term)
            self.filling = filling
    
        def order(self):
            Cake.display(self)
            print(f'Начинка: {self.filling}')
            if Cake.valid_until(self) != 'Срок годности истек':
                print(Cake.valid_until(self))
                print(f'Оформлен заказ {self.id} - {self.name} с начинкой {self.filling} \n')
            else:
                print('Нет в наличии! Выберите другую позицию')
    
    class Cupcake(Pastry):
        def __init__(self, name, price, manufacture_date, term, amount):
            super().__init__(name, price, manufacture_date, term)
            self.amount = amount
    
        def order(self):
            if Cupcake.valid_until(self) != 'Срок годности истек':
                Cupcake.display(self)
                print(f'Количество: {self.amount}')
                print(Cupcake.valid_until(self))
                print(f'Оформлен заказ {self.id} - {self.name}, необходимое количество {self.amount} \n')
            else:
                print('Нет в наличии! Выберите другую позицию')
  ```


## Задача 3

   ```python
class BankAccount:
    def __init__(self, holder, balance, interest_rate):
        self.__holder = holder
        self._balance = balance
        self._interest_rate = interest_rate

    @property
    def holder(self):
        return self.__holder

    @holder.setter
    def holder(self, holder):
        self.__holder = holder

    def __str__(self):
        print(f'Владелец: {self.__holder}')
        print(f'Баланс: ${self._balance:,.2f}')
        print(f'Процентная ставка: {self._interest_rate} \n')

class BankOperation(BankAccount):
    def __init__(self, holder, balance, interest_rate):
        super().__init__(holder, balance, interest_rate)
        self.id = id(self)
        self.transactions = []

    def deposit(self, amount):
        self._balance += amount
        self.transactions.append(f'Аккаунт {self.id} - внесение наличных на счет: ${amount:,.2f}')

    def withdraw(self, amount):
        if self._balance >= amount:
            self._balance -= amount
            self.transactions.append(f'Аккаунт {self.id} - cнятие наличных: ${amount:,.2f}')
        else:
            print('Аккаунт {self.id} - недостаточно средств на счете')

    def add_interest(self):
        interest = self._balance * self._interest_rate
        self._balance += interest
        self.transactions.append(f'Аккаунт {self.id} - начислены проценты по вкладу: ${interest:,.2f}')

    def history(self):
        for transaction in self.transactions:
            print(transaction)
```


## Задача 4

1) Каждый метод `__init__` вызывался только один раз.
Класс Copier унаследован от двух дочерних классов Scanner и Printer, которые, в свою очередь, унаследованы от родительского класса `ComputerDevice`. `ComputerDevice.__init__` не вызывался дважды, потому что мы использовали вызов функции `super()`. В случае, если будет использован другой способ множественного наследования, то метод `ComputerDevice.__init__` будет вызываться в классе `ComputerDevice` два раза. 

```python
  class Copier(Scanner, Printer):
      '''Copy process'''
  
      def __init__(self, inf):
          Scanner.__init__(self, inf)
          Printer.__init__(self, inf)
```

2) Каждый метод `__init__` был запущен до того, как любой из других был завершен.

Важно обращать внимание на момент начала и окончания каждого магического метода `__init__`. В случае, если вы попытаетесь установить атрибут, имя которого конфликтует с другим атрибутом родительского класса, то атрибут будет перезаписан и могут возникнуть ошибки. В данной программе нет конфликта имен с унаследованными атрибутами, поэтому все работает как положено.


## Задача 5
  
```python
   from abc import ABC, abstractmethod

class Investments:
    def __init__(self, ticker, price, currency, industry):
        self.ticker = ticker
        self.price = price
        self.currency = currency
        self.industry = industry

    def __str__(self):
        return f"{self.ticker} ({self.price} {self.currency})"

    @abstractmethod
    def buying(self):
        pass

def buying_securities(func):
    def wrapper(security):
        if security.echelon == 3:
            print('Это высокорискованная сделка')
            return None
        return func(security)
    return wrapper

class Shares(Investments):
    def __init__(self, ticker, price, currency, industry, dividend, echelon, profit):
        super().__init__(ticker, price, currency, industry)
        self.dividend = dividend
        self.echelon = echelon
        self.profit = profit

    @buying_securities
    def buying(self):
        if self.profit > 6:
            lot = input('Количество (лот 10): ')
            return f'Совершена покупка на сумму: {self.price*lot}. Поздравляю Вы стали совладельцем компании!'


class Bonds(Investments):
    def __init__(self, ticker, price, currency, industry, coupon, echelon, nominal):
        super().__init__(ticker, price, currency, industry)
        self.coupon = coupon
        self.echelon = echelon
        self.nominal = nominal

    @buying_securities
    def buying(self):
        if self.price <= self.nominal:
            lot = input('Количество (лот 10): ')
            return f'Совершена покупка на сумму: {self.price * lot}. Поздравляю Вы стали кредитором компании!'


i1 = Shares('GAZP', 174.09, 'RUB', 'Энергетика', True, 1, 1.83)
i2 = Shares('KROT', 2306.80, 'RUB', 'Финансы', True, 3, 701.93)
i3 = Bonds('ОФЗ-26233', 688.75, 'RUB', 'Государственные', 6.1, 1, 1000)
i4 = Bonds('GTLC-3', 1002.3, 'RUB', 'Финансы', 6.95, 3, 1000)

list1 = [i1,i2,i3,i4]

for security in list1:
    print(security.buying())

# Данная информация не является индивидуальной инвестиционной рекомендацией, и финансовые инструменты либо операции, упомянутые в ней, могут не соответствовать Вашему инвестиционному профилю и инвестиционным целям (ожиданиям).
```
