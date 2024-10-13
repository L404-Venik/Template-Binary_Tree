# Задание
исправить работу с памятью в предоставленном шаблонном классе TNode. Оригинал кода - https://mks2.cs.msu.ru/root/pbs_tree

# Исправления:
1. Исправлено использование сырых указателей TNode* в методе Fork. Указатели заменены на TNodePtr. При работе с std::shared_ptr<> стоит использовать только автоматическое управление памятью.
2. Аналогично с конструктором, использующим TNode*.
3. В методах ReplaceLeft и ReplaceRight происходит явное создание умного указателя  std::shared_ptr<TNode<T>>(this).
Заменено на shared_from_this(), это требует того, чтобы класс TNode наследовал std::enable_shared_from_this<TNode<T>>.
При таком наследовании требуется, чтоб конструкторы были публичными, поэтому они вынесены в public.
4. Тип переменной parent заменён на weak_ptr<> чтоб избежать циклических ссылок.
