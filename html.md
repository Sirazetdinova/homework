# HTML

Для продвижения личного бренда люди используют социальные сети или отраслевые пространства, например GitHub или Behance. При этом персональный сайт все еще актуален, не утратил своих преимуществ.
С помощью сайта можно выстраивать личный бренд, продемонстрировать экспертность.

## Задание 

Выполните все пункты задания и сравните с результатом. 

1. Создайте новый HTML документ index.html;
2. В теге body создайте абзац, в котором содержатся три ссылки. Первая ссылка с текстом "Портфолио", вторая ссылка с текстом "Проекты", третья ссылка с текстом "Контакты";
3. После абзаца с ссылками добавьте заголовок первого уровня с текстом специальности, например "Специалист программной инженерии". Добавьте необходимый атрибут к элементу, чтобы осуществить выравнивание заголовка по центру;
4. Используйте HTML-элемент table для представления табличных данных. В первом столбце таблицы разместите фотографию. Во втором столбце в первой строке укажите ФИО, во второй - краткое описание результатов порфессиональной деятельности;

Возможная реализация: 

![s1](img/s1.png)
   
5. Создайте блок с описанем опыта работы. Добавьте заголовок первого уровня "Опыт работы";
6. Добавьте абзац с ненумерованным списоком обязанностей должности;
 
Возможная реализация: 

![s2](img/s2.png)

5. Создайте блок с описанем вашего обучения и пройденных курсов подготовки. Добавьте заголовок первого уровня "Карьерная реализация";
7. Затем создайте блок с описанем лучших проектов. Добавьте заголовок первого уровня "Готовые проекты";
6.  Используйте HTML-элемент table для представления табличных данных;

Возможная реализация: 

![s3](img/s3.png)

![s4](/img/s4.png)


10. Добавьте блок в нижней части страницы. Укажите номер телефона и электронный адрес.
11. У ссылки с номером телефона используйте соответствующий протокол звонка при клике на эту ссылку. У ссылки с e-mail адресом используйте соответствующий протокол написания e-mail письма при клике на эту ссылку.

Возможная реализация: 

![s5](/img/s5.png)

Возможное решение: 

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>personal page</title>
	</head>
		</br>
		<body background="9.jpg">
		<h2 align="center"><font color="#fff" size="5">ИМЯ ФАМИЛИЯ</font>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			<a href="#">ПОРТФОЛИО</a>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			<a href="#">ПРОЕКТЫ</a>
			&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
			<a href="#">КОНТАКТЫ</a>
		</h2>

		<br/>

		<center>
		<h1 align="center"><font color="#fff" size="10">СПЕЦИАЛЬНОСТЬ</font></h1>
			</br>
		<table><tr>
			<td><img style="padding:20px" src="8.jpg" width="450" height="450" alt="Фотография"></td>
			<td>
				<div>
					<h1 align="right"><font color="#fff" size="7">ИМЯ ФАМИЛИЯ </br>ОТЧЕСТВО</font></h1>
					<h2 align="right"><font color="#fff" size="5">
						Веб-разработчик с 4-летним опытом работы. Улучшил<br/>
						процесс разработки, внедрив gitflow, continuous integration.</br>
						Был признан “Работником 2022 года компании Intel”.</br>
						Оптимизировал более 20 000 строк кода PHP. </font>

					</h2>
				</div>
			</td>
		</tr></table>
		</center>

		<br/> <br/> <br/> <br/> <br/> <br/>
		<center>
		<h1 align="center"><font face="Lato" color="#fff" size="10">Опыт работы</font></h1>
			<table>
			<tr>
				<td><div><h2 align="center"><font face="Lato" color="#fff" size="5">2023 | ООО "Финансовый помощник"</font></h2></div></td>
			<td>
				<div><h2 align="center"><font face="Lato" color="#fff" size="5">Архитектор СУБД (Разработчик 1С)</font></h2></div>
				<div><ul class="list"><font face="Lato" color="#fff" size="4">
					<li><h3>Проектирование архитектуры баз учета (1С 8.2, SQL 2005-2008)</h3></li>
					<li><h3>Составление ТЗ</h3></li>
					<li><h3>Описание бизнес-процессов</h3></li>
					<li><h3>Оптимизация программного кода</h3></li>
					<li><h3>Непосредственное участие в разработке и внедрении ПО</h3></li>
				</font></ul></div>
			</td>
			</tr>

			<tr>
			<td><div><h2 align="center"><font face="Lato" color="#fff" size="5">2020 | ООО «Техпром»</font></h2></div></td>
			<td>
				<div><h2 align="center"><font face="Lato" color="#fff" size="5">Программист</font></h2></div>
				<div><ul class="list"><font face="Lato" color="#fff" size="4">
					<li><h3>Сбор и формализация требований к системе</h3></li>
					<li><h3>Разработка основного функционала системы</h3></li>
					<li><h3>Постановка задач фрилансерам</h3></li>
					<li><h3>Контроль выполнения</h3></li>
					<li><h3>Организация тестирования</h3></li>
					<li><h3>Обучение пользователей</h3></li>
					<li><h3>Обслуживание серверов компании</h3></li></font>
				</ul></div>
			</td>
			</tr>

		</table>
		</center>

		<br/> <br/>
		<center>
		<h1 align="center"><font face="Lato" color="#fff" size="6">Карьерное развитие</font></h1>
			<table>
			<tr>
				<td><div><h2 align="center"><font face="Lato" color="#fff" size="5">2022-2028 | Университет</font></h2></div></td>
			<td>
				<div><h2 align="right"><font face="Lato" color="#fff" size="5">
					Направление готовит разработчиков, которые владеют </br>
					современными технологиями разработки ПО и несколькими</br>
					языками программирования, с первого курса работают над </br>
					реальными задачами. Изучаемые ЯП — С++, Python, Java, </br>
					Haskell и Kotlin. </font></h2></div>
				<div><ul class="list"><font face="Lato" color="#fff" size="4">
					<li><h3><b>Учебное заведение:</b> ВВВВ</h3></li>
					<li><h3><b>Направление:</b> Прикладная математика и информатика</h3></li>
				</font></ul></div>
			</td>
			</tr>

		</table>
		</center>

<br/><br/>

		<center>
		<h1 align="center"><font face="Lato" color="#fff" size="6">Курсы по работе с искусственным интеллектом</font></h1>
			<table>
			<tr>
				<td><div><h2 align="center"><font face="Lato" color="#fff" size="5">2018-2020 | AI Data Scientist</font></h2></div></td>
			<td>
				<div><h2 align="right"><font face="Lato" color="#fff" size="5">
					Курс предполагает работу с огромным объёмом </br>
					неструктурированной информации. В работе применяют</br>
					математическую статистику и методы машинного </br>
					обучения. Специалист анализирует Big Data и </br>
					делает прогнозную модуль.</font></h2></div>
				<div><ul class="list"><font face="Lato" color="#fff" size="4">
					<h3><b>Документ об успешном окончании:</b> Сетификат</h3>
				</font></ul></div>
			</td>
			</tr>

			<tr>
				<td><div><h2 align="center"><font face="Lato" color="#fff" size="5">2020-2021 | Machine Learning</font></h2></div></td>
			<td>
				<div><h2 align="right"><font face="Lato" color="#fff" size="5">
					Направление искусственного интеллекта, сосредоточенное</br>
					на создании систем, которые обучаются и развиваются на</br>
					основе получаемых ими данных.</font></h2></div>
				<div><ul class="list"><font face="Lato" color="#fff" size="4">
					<h3><b>Документ об успешном окончании:</b> Сетификат</h3>
				</font></ul></div>
			</td>
			</tr>
		</table>


		<center>
		<h1 align="center"><font face="Lato" color="#fff" size="10">Готовые проекты</font></h1>
		<table><tr>
			<td><img style="padding: 50px;" src="10.jpg" width="300" height="200" alt="Фотография"></td>
			<td>
				<div>
					<h2><font face="Lato" color="#fff" size="7">Конкурентная структура данных</font></h2>
					<h3><font face="Lato" color="#fff" size="5">
						Рассмотрена реализация относительно нового подхода к </br>
						построению конкурентных структур данных – подход на </br>
						временных метках. Рассматриваются возможности </br>
						освобождения памяти и использования структуры данных </br>
						на временных метках с неограниченным числом потоков.
					</font></h3>
				</div>
			</td>
		</tr></table>
		<br/> <br/>
		<table><tr>
			<td>
				<div>
					<h2><font face="Lato" color="#fff" size="7">Биометрическая аутентификация</font></h2>
					<h3><font face="Lato" color="#fff" size="5">
						Проверка подлинности на основе биометрических показателей. <br/>
						При биометрической аутентификации, секретными данными пользователя<br/>
						служит отпечаток пальца.Образ обеспечивает высокий уровень защиты <br/>
						доступа к информации.
						</font></h3>
				</div>
			</td>
			<td><img style="padding: 50px;" src="10.jpg" width="300" height="200" alt="Фотография"></td>
		</tr></table>
		<br/><br/>
		<table><tr>
			<td><img style="padding: 50px;" src="10.jpg" width="300" height="200" alt="Фотография"></td>
			<td>
				<div>
					<h2><font face="Lato" color="#fff" size="7">Шифрование изображений с </br> использованием алгоритма AES</font></h2>
					<h3><font face="Lato" color="#fff" size="5">
						Симметричный алгоритм блочного шифрования, который оперирует<br/>
						блоками по 128 бит. AES берет 128 бит исходного сообщения и <br/>
						превращает их с помощью некоего ключа в 128-битный шифротекст.</font></h3>
				</div>
			</td>
		</tr></table>
		</center>

		<footer class="footer">
			<h3 align="center"><font face="Lato" color="#fff" size="6">Контакты</font></h3>
			<center>
			<address>
				<p><a href="tel:+7 (917) 372-89-23"><font face="Lato" color="#fff" size="4">Телефон: +7 (917) 372-89-23</font></a></p>
				<p><a href="mailto:vlad@webref.ru"><font face="Lato" color="#fff" size="4">Email: hello@website.ru</font></a></p>
			</address>
			</center>
		</footer>
		</center> 
		</body>
</html>
```
