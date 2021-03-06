---
layout: post
title: Обновления в расписании и задание №0
---
 
Добрый вечер, уважаемые студенты. 
По этой [ссылке](https://b1kers.github.io) я буду выкладывать задачи и другую информацию. Все обновления буду сопровождать письмами на почту групп.

## Расписание 
Для группы 18210: ваша пара теперь во вторник, в 9:00 в т4214 (вообще мне говорили про т4220, но если что, они рядом)

## Ссылка на материалы
Всеволод Юрьевич наверняка даст на лекции [ссылку](https://www.sites.google.com/site/nguoop/)
Там можно найти слайды лекций, доп. литературу и задачи с прошлого года. Основные, зачётные задачи этого года для ваших групп я выложу до конца этой недели после согласования с другими преподавателями.

Ваше вводное, нулевое задание приведено ниже.

## Задача №0
Вам нужно будет познакомиться с раздельной компиляцией и пространством имен в C++. В качестве примера используйте следующую программу:

Файл _module1.h_:
```cpp
#include <string>

namespace Module1
{
	std::string getMyName();
}
```

Файл _module1.cpp_:
```cpp
#include "module1.h"

namespace Module1
{
	std::string getMyName()
	{
		std::string name = "John";
		return name;
	}
}
```

Файл _module2.h_:
```cpp
#include <string>

namespace Module2
{
	std::string getMyName();
}
```
Файл _module2.cpp_:
```cpp
#include "module2.h"

namespace Module2
{
	std::string getMyName()
	{
		std::string name = "James";
		return name;
	}
}
```
Файл _main.cpp_:
```cpp
#include "module1.h"
#include "module2.h"
#include <iostream>

int main(int argc, char** argv)
{
	std::cout <<  "Hello world!" << "\n";
	
	std::cout << Module1::getMyName() << "\n";
	std::cout << Module2::getMyName() << "\n";

	using namespace Module1;
	std::cout << getMyName() << "\n"; // (A)
	std::cout << Module2::getMyName() << "\n";

	//using namespace Module2; // (B)
	//std::cout << getMyName() << "\n"; // COMPILATION ERROR (C)

	using Module2::getMyName;
	std::cout << getMyName() << "\n"; // (D)

}
```
С тестовой программой нужно выполнить следующие действия:
1. Собрать программу и убедиться, что на каждый *.cpp файл создается отдельный объектный файл с тем же именем (для Visual Studio, например, в папке Debug будут создаваться файлы с расширением *.obj, AFAIK в CLion аналогично). 

2. Убедиться, что при изменении одного *.cpp файла и пересборке проекта обновляется только соответствующий ему объектный файл (дата изменения других объектных файлов останется прежней)

3. Объяснить, что выведется при выполнении строк с комментариями (А) и (D) в main.cpp

4. Убедиться, что раскомментирование строк (B) и (C) в main.cpp приводит к ошибке компиляции. Объяснить, почему эта ошибка происходит, и предложить пути её устранения.

5. Добавить в программу еще одну функцию getMyName(), возвращающую имя Peter. Обернуть её в еще одно пространство имён.

6. Объяснить, как можно избавиться от необходимости писать std::cout и вместо этого писать просто cout.
