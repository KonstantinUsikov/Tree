# Tree — реализации деревьев на C#

Учебный проект с реализациями древовидных структур данных на C# (.NET Framework 4.8) и консольным приложением для их демонстрации.

## Структура решения

```
Tree.sln
├── ClassLibraryTree/   — библиотека классов со структурами данных
└── ConsoleAppTree/     — консольное приложение (Program.cs), использующее библиотеку
```

## Реализованные структуры

| Класс | Файл | Описание |
|-------|------|----------|
| `BinaryTree`, `Node` | `BinaryTree.cs` | Бинарное дерево поиска на связанных узлах (с указателем на родителя). Вставка, поиск, минимум/максимум, удаление (`Delete`, `Delete_NR`), следующий/предыдущий элемент (`Search_Next`, `Search_Prev`), очистка дерева (`Clear`). |
| `BinaryTreeArray` | `BinaryTreeArray.cs` | Бинарное дерево поиска, хранящееся в массиве: потомки узла `i` находятся по индексам `2i+1` и `2i+2`, пустая ячейка помечается константой `INF`. Массив расширяется по уровням. |
| `AVLTree` | `AVLTree.cs` | АВЛ-дерево (самобалансирующееся). Высоты узлов, коэффициент баланса (`GetBalance`), малые левый/правый повороты, балансировка при вставке и удалении. Использует класс `Node`. |
| `OptimalBST`, `OptimalBSTNode` | `BinaryTreeOptimal.cs` | Построение оптимального дерева поиска по ключам и их вероятностям методом динамического программирования (`BuildOptimalBST`). |
| `BTree<T>`, `BTreeNode<T>` | `BTree.cs` | Обобщённое B-дерево (`T : IComparable<T>`) заданной степени. Вставка с разделением узлов, вывод дерева с отступами (`Print`). |
| `LeftChildRightSiblingTree`, `TreeNode` | `LeftChildRightSiblingTree.cs` | Дерево с произвольным числом потомков в представлении «левый ребёнок — правый брат». Добавление потомка (`AddChild`), обход (`Traverse`). |

## Соглашение об именовании

Многие операции реализованы в двух вариантах:

- `_R` — рекурсивная версия (например, `Insert_R`, `Search_R`, `GetMin_R`);
- `_NR` — нерекурсивная версия (например, `Insert_NR`, `Search_NR`, `GetMin_NR`), обходы используют явный стек.

## Обходы

`BinaryTree`, `BinaryTreeArray` и `AVLTree` поддерживают три вида обхода, каждый в вариантах `_R` и `_NR`:

| Обход | Методы |
|-------|--------|
| Прямой (pre-order) | `PreOrder_R`, `PreOrder_NR` |
| Симметричный (in-order) | `InOrder_R`, `InOrder_NR` |
| Обратный (post-order) | `PostOrder_R`, `PostOrder_NR` |

Методы возвращают строку со значениями узлов, разделёнными пробелами.

## Требования

- Windows
- .NET Framework 4.8 Developer Pack (пакет нацеливания; без него сборка завершится ошибкой `MSB3644`) — https://aka.ms/msbuild/developerpacks
- Visual Studio 2019+ или JetBrains Rider

## Сборка и запуск

**В IDE:** откройте `Tree.sln`, выберите `ConsoleAppTree` в качестве запускаемого проекта и запустите его.

**Из командной строки:**

```
msbuild Tree.sln
ConsoleAppTree\bin\Debug\ConsoleAppTree.exe
```

## Пример использования

```csharp
using ClassLibraryTree;

BinaryTree binTree = new BinaryTree();
List<int> items = new List<int>() { 21, 7, 32, 5, 14, 27, 37, 4, 6, 12, 18, 25, 30, 34, 39, 2, 9, 24, 33 };
foreach (int item in items)
    binTree.Insert_R(binTree.root, item);

Console.WriteLine(binTree.InOrder_R(binTree.root));
```

Вывод — элементы в порядке возрастания:

```
2 4 5 6 7 9 12 14 18 21 24 25 27 30 32 33 34 37 39
```

В `ConsoleAppTree/Program.cs` также есть закомментированные примеры для `OptimalBST`, `LeftChildRightSiblingTree` и `BTree<T>`. Чтобы запустить их, раскомментируйте нужный блок.
