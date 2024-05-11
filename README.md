## Laboratory work II


### Part I

1. **Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).**
2. **Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.**


```bash
	
mkdir lab_2 && cd lab_2
git init
git remote add origin git@github.com:PhilippD3/lab02.git
git pull origin main
git branch -m main
	
```
	
	
3. **Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу "Hello world" на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.**


```bash
cat > hello_world.cpp << EOF
```

```cpp
#include <iostream>

using namespace std;


int main() 
{

cout << "Hello,World! " << endl;

return 0;
}
```

```bash
EOF
```


4. **Добавьте этот файл в локальную копию репозитория.**


``` bash

git add hello_world.cpp

```


5. **Закоммитьте изменения с *осмысленным* сообщением.**


```bash 

git commit -m "add hello_world.cpp"

```


6. **Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.**


```bash
cat > hello_world.cpp << EOF
```
```cpp 
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string name;
    
    getline(cin, name);
    
    
    cout<<"Hello World from " << name;

    return 0;
}
```
```
EOF
```

7. **Закоммитьте новую версию программы.** Почему не надо добавлять файл повторно `git add`?


```bash

 git add hello_world.cpp
 git commit -m "add hello_world v2.0"

```


8. **Запуште изменения в удалёный репозиторий.**


```bash

git push origin main

```


10. **Проверьте, что история коммитов доступна в удалёный репозитории.**





### Part II
**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*


1. **В локальной копии репозитория создайте локальную ветку `patch1`.**


```bash

git checkout -b patch1

```


2. **Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.**


```bash
cat > hello_world.cpp << EOF
```

```cpp
#include <iostream>
#include <string>


int main()
{
    std::string name;

    getline(std::cin, name);


    std::cout<<"Hello World from " << name;

    return 0;
}
```
```
EOF
```

3. **commit, push локальную ветку в удалённый репозиторий.**


```bash 

git add hello_world.cpp
git commit -m "hello_world.cpp without using namespace std;"
git push origin patch1

```


4. **Проверьте, что ветка `patch1` доступна в удалёный репозитории.**



5. **Создайте pull-request `patch1 -> master`.**


6. **В локальной копии в ветке `patch1` добавьте в исходный код комментарии.**


```bash
cat > hello_world.cpp << EOF
```

```cpp
#include <iostream>
#include <string>


int main()
{
    std::string name;

    //name input
    getline(std::cin, name);

    //name output
    std::cout<<"Hello World from " << name;

    return 0;
}

```
```
EOF
```


7. **commit**, **push**.
```bash
git add hello_world.cpp
git commit -m "Comments"
git push origin patch1
```
8. **Проверьте, что новые изменения есть в созданном на **шаге 5_pull-request**




9. **удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.**

10. Локально выполните **pull**.


```bash

git checkout main
git pull origin main

```


11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.


```bash

git log

```
```
ommit d4f86cf7a4757dd31e0a2be7d915f7557b0fcab5 (HEAD -> main, origin/main)
Author: PhilippD3 <filipp.sadkov@mail.ru>
Date:   Sat May 11 12:53:02 2024 +0300

    add hello_world v2.0

commit 08bd15492d5474a5a0555f57a38289b5dbad148b
Author: PhilippD3 <filipp.sadkov@mail.ru>
Date:   Sat May 11 12:42:00 2024 +0300

    add hello_world.cpp
```


12. Удалите локальную ветку `patch1`.


```bash

git branch -D patch1
Deleted branch patch1 (was 13c1c36).

```




### Part III
**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*


1. **Создайте новую локальную ветку `patch2`.**


```bash

git checkout -b patch2

```


2. **Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.**


```bash

clang-format  -style=Mozilla hello_world.cpp 

```


3. **commit, push, создайте pull-request `patch2 -> master`**.


```bash

git add hello_world.cpp
git commit -m "Mozilla codestyle"
git push origin patch2

```


4. **В ветке "master" в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.**


5. **Убедитесь, что в pull-request появились 'конфликтны'.**


6. **Для этого локально выполните pull + rebase (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.**


```bash

git pull origin main
git rebase main

```


7. **Сделайте *force push* в ветку `patch2`**

```bash

git push --force origin patch2

```


8. **Убедитель, что в pull-request пропали конфликтны.**


9. **Вмержите pull-request `patch2 -> master`.**
