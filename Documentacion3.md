# Documentacion Doble Lista Enlazada
## Alan Albino Tellez Giron Lizarraga

### DLList.h
```c++
#include <utility>
#include <iostream>
```
Se mandan a llamar las bibliotecas utility e iostream
```c++
template <typename Object>
class DLList {
private:
    struct Node {
        Object data;
        Node *prev;
        Node *next;

        Node(const Object &d = Object{}, Node *p = nullptr, Node *n = nullptr);
        Node(Object &&d, Node *p = nullptr, Node *n = nullptr);
    };
```
* Aqui primero se define la clase DLList que representa la lista doblemente enlazada.
Dentro de la clase hay una estructura interna llamada Node que representa un nodo de la lista
  * Cada nodo tiene 3 campos
    * data 
      * Campo para almacenar los datos del nodo
    * prev
      * Un puntero al nodo anterior en la lista
    * next
      * Un puntero al nodo de la siguiente en la lista
* Despues de la definicion de la estructura Node hay dos constructores definidos para la estructura Node.
  * Uno toma una referencia constante a un objeto y dos punteros para el nodo anterior y siguiente respectivamente
  * El otro constructor toma un objeto de tipo Object por movimiento y dos punteros para el nodo anterior y siguiente respectivamente
```c++
public:
    class const_iterator{
    public:
        const_iterator();
        const Object &operator*() const;
        const_iterator &operator++();
        const_iterator operator++ (int);
        bool operator== (const const_iterator& rhs) const;
        bool operator!= (const const_iterator& rhs) const;

    protected:
        Node* current;
        Object& retrieve() const;
        const_iterator(Node *p);

        friend class DLList<Object>;
    };
```
* Este codigo define una clase const_iterator dentro de la clase DLList. Esta clase representa un iterador constante para la
lista doblemente enlazada. Un iterador constante permite recorrer la lista y acceder a los elementos de la lista, pero no 
permite modificar los datos que apunta el iterador.

```c++
const_iterator()
```
* Constructor por defecto de la clase
```c++
const Object &operator*() const
```
* Sobrecarga del operador de desreferenciacion para acceder al valor del nodo actual al que apunta el iterador
```c++
const_iterator &operator++()
```
* Sobrecarga del operador de incremento prefijo
```c++
const_iterator operator++ (int)
```
* Sobrecarga del operador de incremento sufijo
```c++
bool operator == (const const_iterator& rhs const)
```
* Sobrecarga del operador de igualdad
```c++
bool operator != (const const_iterator& rhs) const
```
* Sobrecarga del operador de desigualdad
```c++
Node* current
```
* Puntero al nodo actual al que apunta el iterador
```c++
Object& retrieve() const 
```
* Funcion auxiliar que devuelve una referencia al objeto contenido en el nodo actual al que apunta el iterador.
```c++
const_iterator(Node *p)
```
* Constructor protegido que crea un iterador con un puntero a un nodo dado

```c++
 class iterator : public const_iterator {
    public:
        iterator();
        Object& operator*();
        const Object& operator*() const;
        iterator & operator++ ();
        iterator &operator--();
        iterator operator++ (int);
        iterator operator-- (int);
        iterator operator+ (int steps) const;

    protected:
        iterator(Node *p);

        friend class DLList<Object>;
    };
```
* esta es una subclakse de cont_iterator, lo que significa que hereda todos los miembros y funciones miembro de const_iterador
y ademas añade funcionalidades adicionales que permiten la modifican de los elementos de la lista.
```c++
const_iterator()
```
* Constructor por defecto de la clase
```c++
Object& operator*()
```
* Sobrecarga del operador de desreferenciacion
```c++
const Object& operator*() const
```
* Sobrecarga del operador de desreferenciacion
```c++
iterator & operator++ ()
```
* Sobrecarga del operador de incremento prefijo
```c++
iterator &operator--()
```
* Sobrecarga del operador de decremento prefijo
```c++
iterator operator++ (int)
```
* Sobrecarga del operador de incremento sufijo
```c++
iterator operator-- (int)
```
* Sobrecarga del operador de decremento sufijo
```c++
iterator operator+ (int steps)
```
* Sobrecarga del operador de suma
```c++
iterator(Node *p)
```
* Constructor protegido que crea un iterador con un puntero a un nodo dado.
```c++
public:
    DLList();
    DLList(std::initializer_list<Object> initList);
    ~DLList();
    DLList(const DLList &rhs);
    DLList &operator=(const DLList &rhs);
    DLList(DLList &&rhs);
    DLList &operator=(DLList &&rhs);

    iterator begin();
    const_iterator begin() const;
    iterator end();
    const_iterator end() const;

    int size() const;
    bool empty() const;

    void clear();

    Object &front();
    const Object &front() const;
    Object &back();
    const Object &back() const;

    void push_front(const Object &x);
    void push_front(Object &&x);
    void push_back(const Object &x);
    void push_back(Object &&x);

    void pop_front();
    void pop_back();

    iterator insert(iterator itr, const Object &x);
    iterator insert(iterator itr, Object &&x);

    void insert(int pos, const Object &x);
    void insert(int pos, Object &x);

    iterator erase(iterator itr);
    void erase(int pos);
    iterator erase(iterator from, iterator to);

    void print() const;

private:
    int theSize;
    Node *head;
    Node *tail;

    void init();
    iterator get_iterator(int pos);
};
```
* Este codigo define una clase DLList que representa una lista doblemente enlazada
```c++
DLList()
```
* Constructor predeterminado que crea una lista vacia
```C++
DLList(std::initializer_list<Object> initList)
```
* Constructor que crea una lista a partir de una lista de incializacion de objetos
```c++
~DLList()
```
* Destructor que libera la memoria utilizada por la lista
```c++
DLList(const DLList &rhs)
```
* Constructor de copia que crea una copia profunda de otra lista.
```c++
DLList(DLList &&rhs)
```
* Constructor de movimiento que mueve los recursos de otra lista
```c++
DLList &operator =(DLList &&rhs)
```
* Operatos de asignacion de movimiento que mueve los recursos de otra lista
```c++
iterator begin()
```
* Funcion que devuelve un iterador al primer elemento de la lista
```C++
iterator end()
```
* Funcion que devuelve un iterador al final de la lista
```C++
const_iterator end() const
```
* Funcion que devuelve un iterador constante al final de la lista
```c++
int size() const
```
* Funcion que devuelve el numero de elementos en la lista
```C++
bool empty() const
```
* Funcion que devuelve true si la lista esta vacia
```c++
void clear()
```
* Funcion que elimina todos los elementos de la lista.
```c++
Object &front() const
```
* Funcion que devuelve una referencia al primer elemento de la lista
```c++
const Object &front() const
```
* Funcion que devuelve una referencia constante al primer elemento de la lista
```c++
Object &back()
```
* Funcion que devuelve una referencia al ultimo elemento de la lista
```c++
const Object &back() const
```
* Funcion que devuelve una referencia constante al ultimo elemento de la lista
```c++
void push_front(const Object &x)
```
* Funcion que inserta un elemento al final de la lista
```c++
void push_front(Object &&x)
```
* Funcion que inserta un elemento al final de la lista utilizando la semantica de movimiento
```c++
void push_back(const Object &x)
```
* Funcion que inserta un elemento al final de la lista
```c++
void push_back(const Object &&x)
```
* Funcion que inserta un elemento al final de la lista utilizando la semantica de movimiento
```c++
void pop_front()
```
* Funcion que elimina el primer elemento de la lista
```c++
void pop_back()
```
* Funcion que elimina el ultimo elemento de la lista
```c++
iterator insert(iterator itr, const Object &x)
```
* Funcion que inserta un elemento antes de la posicion indicada por un iterador
```c++
iterator insert(iterator itr, Object &&x)
```
* Funcion que inserta un elemento antes de la posicion indicada por un iterador utilizando la semantica de movimiento
```c++
void insert(int pos, const Object &x)
```
* Funcion que inserta un elemento en una posicion especifica
```c++
void insert (int pos, Object &x)
```
* Funcion que inserta un elemento en una posicion especifica utilizando la semantica de movimiento
```c++
iterator erase(iterator itr)
```
* Funcion que elimina un elemento apuntado por un iterador y devuelve un iterador apuntando al siguiente elemento
```c++
void erase (int pos)
```
* Funcion que elimina un elemento en la posicion especificada
```c++
iterator erase(iterator from, iterator to)
```
* Funcion que elimina los elementos en el rango y devuelve un iterador apuntando al siguiente elemento despues del ultimo eliminado
```c++
void print() const
```
* Funcion que implime los elementos de la lista

### DLList.cpp

```c++
template<typename Object>
DLList<Object>::Node::Node(const Object &d, Node *p, Node *n)
        : data{d}, prev{p}, next{n} {}
```
* Este es el constructor de la clase node que esta anidado dentro de la clase DLList
  * Este constructor contiene 3 parametros
    * Const Object &d
      * Es una referencia constante al objeto que se almacenara en el nodo
    * Node *p
      * Es un puntero al nodo previo en la lista
    * Node *n
      * Es un puntero al siguiente nodo en la lista
```c++
template<typename Object>
DLList<Object>::Node::Node(Object &&d, Node *p, Node *n)
        : data{std::move(d)}, prev{p}, next{n} {}
```
* Este constructor crea un nodo para la lista doblemente enlazada utilizando una referencia de valor r del objeto

```c++
template<typename Object>
DLList<Object>::const_iterator::const_iterator() : current{nullptr} {}
```
* Este es el constructor predeterminado de la clase const_iterator dentro de la clase DLList
```c++
current{nullptr}
```
* Inicializa el puntero current con el valor nullptr
  * Este puntero se utiliza para apuntar al nodo actual al que esta haciendo referencia el iterador
```c++
template<typename Object>
const Object &DLList<Object>::const_iterator::operator*() const {
    return retrieve();
}
```
* Este es el operador de la desreferenciacion de la clase const_iterator de la clase DLList
```c++
const Object &
```
* Esto especifica que el operdor devuelve una referencia constante al objeto almacenado en el nodo al que apunta eliterador.
```c++
DLList<Object>::const_iterator::retrieve()
```
* Llama a la funcion miembro retrieve para obtener el objeto al que apunta el iterador.
```c++
template<typename Object>
typename DLList<Object>::const_iterator &DLList<Object>::const_iterator::operator++() {
    current = current->next;
    return *this;
}
```
* Este es el operador de preincremento de la clase const_iteratos dentro de la clase DLList, este operador de preincremento
se utiliza para avanzar el iterador al siguiente elemento en la lista enlazada doble
```c++
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::const_iterator::operator++(int) {
    const_iterator old = *this;
    ++(*this);
    return old;
}
```
* Este es el operador de postincremento de la clase const_iterator dentro de la clase DLList, este operador de postincremento
devuelve unma copia del iterador antes que se haya incrementado
```c++
template<typename Object>
bool DLList<Object>::const_iterator::operator==(const const_iterator &rhs) const {
    return current == rhs.current;
}
```
* Este es el operador de igualdad de la clase const_iterator dentro de la clase DLList, este operador se utiliza para comparar
dos iteradores de la lista enlazada doble y determinar si apuntan al mismo nodo en la lista
```c++
template<typename Object>
bool DLList<Object>::const_iterator::operator!=(const const_iterator &rhs) const {
    return !(*this == rhs);
}
```
* Este es el operador de desigualdad de la clase const_iterator dentro de la clase DLList, este operador se usa para verificar
si 2 iteradores de la lista enlazada doble son diferentes
```c++
template<typename Object>
Object &DLList<Object>::const_iterator::retrieve() const {
    return current->data;
}
```
* Este es el metodo privado retrieve() de la clase const_iterator dentro de la clase DLList, este metodo se utiliza internamente
para obtener el objeto al que apunta el iterador.
```c++
template<typename Object>
DLList<Object>::const_iterator::const_iterator(Node *p) : current{p} {}
```
* Este es el constructor de la clase const_iterator dentro de la clase DLList que toma un puntero a un nodo como argumento para
inicializar el iterador.
```c++
template<typename Object>
DLList<Object>::iterator::iterator() {}
```
* Este es el constructor predeterminado de la clase iterator dentro de la clase DLList
```c++
template<typename Object>
Object &DLList<Object>::iterator::operator*() {
    return const_iterator::retrieve();
}
```
* Este es el operador de desreferenciacion de la clase iterator dentro de la clase DLList, Dado que iterator es una subclase
de const_iterator puede acceder a los metodos y miembros protegidos de la clase base. El metodo retrieve se llama a traves de
la clase base const_iterator, lo que permite al iterator acceder al objeto almacenado en el nodo actual de la misma manera que lo
haria un const_iterator
```c++
template<typename Object>
const Object &DLList<Object>::iterator::operator*() const {
    return const_iterator::operator*();
}
```
* Este es el operador de desrefernciacion constante de la clase iterator dentro de la clase DLList. Dado que iterator es
una subclase de const_iterator, puede acceder a los metodos y miembros protegidos de la clase base.
```c++
template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator++() {
    this->current = this->current->next;
    return *this;
}
```
* Este es el operador de preincremento de la clase iterator dentro de la clase DLList, este operador de preincremento se utiliza
para avanzar el iterador al siguiente elemento en la lista enlazada doble.
```c++
template<typename Object>
typename DLList<Object>::iterator &DLList<Object>::iterator::operator--() {
    this->current = this->current->prev;
    return *this;
}
```
* Este es eñ péradpr de predecremento de la clase iterator dentro de la clase DLList, este operador de predecremento
se utiliza para retroceder el iterador al nodo previo en la lista enlazada doble
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator++(int) {
    iterator old = *this;
    ++(*this);
    return old;
}
```
* Este el operador de postincremento de la clase iterator dentro de la clase DLList, este operador de postincremento devuelve una
copia del iterador antes de que se haya incrementado.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator--(int) {
    iterator old = *this;
    --(*this);
    return old;
}
```
* Este es el operador de postdecremento de la clase iterator dentro de la clase DLList, este operador de postdecremento
devuelve una copia del iterador antes de que se haya decrementado.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::iterator::operator+(int steps) const {
    iterator new_itr = *this;
    for(int i = 0; i < steps; ++i) {
        ++new_itr;
    }
    return new_itr;
}
```
* Este es el operador de suma de la clase iterator dentro de la clase DLList, este operador se utiliza para avanzar el iterador
actual en un numero especifico de pasos hacia adelante.
```c++
template<typename Object>
DLList<Object>::iterator::iterator(Node *p) : const_iterator{p} {}
```
* Este es el constructor de la clase iterator, que toma un puntero a un nodo como argumento para inicializar el iterador,
que toma un puntero a un nodo como argumento para inicializar el iterador, este constructor llama al constructor de la clase
base const_iterator para inicializar la parte del iterator que hereda de const_iterator
```c++
template<typename Object>
DLList<Object>::DLList() : theSize{0}, head{new Node}, tail{new Node} {
    head->next = tail;
    tail->prev = head;
}
```
* Este es el constructo predeterminado de la clase DLList, que inicializa una lista doblemente enlazada vacia, esto crea una
lista doblemente enlazada vacia con un nodo head y un nodo tail, donde el head apunta al tail y el tail apunta al head.
```c++
template<typename Object>
DLList<Object>::DLList(std::initializer_list<Object> initList) : DLList() {
    for(const auto &item : initList) {
        push_back(item);
    }
}
```
* Este es el constructor de la clase DLList que toma una lista de inicializacion como argumento para inicializar la lista
doblemente enlazada con los elementos de la lista proporcionada
```c++
template<typename Object>
DLList<Object>::~DLList() {
    clear();
    delete head;
    delete tail;
}
```
* Este es eñ destructor de la clase DLList responsable de liberar la memoria utilizada por la lista doblemente enlazada.
```c++
template<typename Object>
DLList<Object>::DLList(const DLList &rhs) : DLList() {
    for(auto &item : rhs) {
        push_back(item);
    }
}
```
* Este es el constructor de copia de clase DLList que crea una nueva lista doblemente enlazada copiando los elementos de
otra lista doblemente enlazada proporcionada como argumento.
```c++
template<typename Object>
DLList<Object> &DLList<Object>::operator=(const DLList &rhs) {
    DLList copy = rhs;
    std::swap(*this, copy);
    return *this;
}
```
* Este es el operador de asignacion de la clase DLList que asigna los contenidos de otra lista doblemente enlazada a la lista
actual.
```c++
template<typename Object>
DLList<Object>::DLList(DLList &&rhs) : theSize{rhs.theSize}, head{rhs.head}, tail{rhs.tail} {
    rhs.theSize = 0;
    rhs.head = nullptr;
    rhs.tail = nullptr;
}
```
* Este es el constructor de movimiento de la clase DLList que realiza la transferencia de recrusos de otra lista doblemente enlazada
a la lista actual.
```c++
template<typename Object>
DLList<Object> &DLList<Object>::operator=(DLList &&rhs) {
    std::swap(theSize, rhs.theSize);
    std::swap(head, rhs.head);
    std::swap(tail, rhs.tail);
    return *this;
}
```
* Este es el operador de asignacion de movimiento de la clase DLList, que realiza la transferencia de recursos desde otra
lista doblemente enlazada a la lista actual.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::begin() {
    return {head->next};
}
```
* Este es el metodo begin() de la clase DLList que devuelve un iterador que apunta al primer elemento de la lista.
```c++
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::begin() const {
    return {head->next};
}
```
* Este es el metodo begin() constante de la clase DLList, que devuelve un iterador contante que apunta al primer elemento de la lista.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::end() {
    return {tail};
}
```
* Este es el metodo end() de la clase DLList, que devuelve un iterador que apunta al elemento despues del ultimo elemento de la lista.
```c++
template<typename Object>
typename DLList<Object>::const_iterator DLList<Object>::end() const {
    return {tail};
}
```
* Este es el metodo end() constante de la clase DLList que devuelve un iterador constante que apunta al elemento despues del ultimo
elmento de la lista.
```c++
template<typename Object>
int DLList<Object>::size() const {
    return theSize;
}
```
* Este es el metodo size de la clase DLList que devuelve el tamaño actual de la lista, este metodo proporciona una forma de obtener
el tamaño actual de la lista doblemente enlazada.
```c++
template<typename Object>
bool DLList<Object>::empty() const {
    return size() == 0;
}
```
* Este es el metodo empty de la clase DLList, que devuelve un valor booleano indicando si la lista esta vacia o no, este metodo
proporciona una forma conveniente de verificar si la lista doblemente enlazada esta vacia o no.
```c++
template<typename Object>
void DLList<Object>::clear() {
    while(!empty()) {
        pop_front();
    }
}
```
* Este el metodo clear de la clase DLList, que elimina todos los elementos de la lista doblemente enlazada
```c++
template<typename Object>
Object &DLList<Object>::front() {
    return *begin();
}
```
* Este el metodo front() de la clase DLList, que devuelve una referencia al primer elemento de la lista doblemente enlazada, este
metodo proporciona una forma conveniente de acceedr al primer elemento de la lista doblemente enlazada.
```c++
template<typename Object>
const Object &DLList<Object>::front() const {
    return *begin();
}
```
* Este es el metodo front constante de la clase DLList, que devuelve una referencia constante al primer elemento de la lista doblemente enlazada
```c++
template<typename Object>
Object &DLList<Object>::back() {
    return *(--end());
}
```
* Este es el metodo back de la clase DLList que devuelve una referencia al ultimo elemento de la lista doblemente enlazada,
este metodo proporciona una forma conveniente de acceder al ultimo elemento de la lista doblemente enlazada.
```c++
template<typename Object>
const Object &DLList<Object>::back() const {
    return *(--end());
}
```
* Este es el metodo back constante de la clase DLList que devuelve una referencia constante al ultimo elemento de la lista doblemente
enlazada.
```c++
template<typename Object>
void DLList<Object>::push_front(const Object &x) {
    insert(begin(), x);
}
```
* Este es el metodo push_front() de la clase DLList que inserta un nuevo elemento al frente de la lista doblemente enlazada con el valor proporcionado
```c++
template<typename Object>
void DLList<Object>::push_front(Object &&x) {
    insert(begin(), std::move(x));
}
```
* Este es el metodo push_front de la clase DLList que inserta un nuevo elemento al frente de la lista doblemente enlazada utilizando
una referencia de movimiento
```c++
template<typename Object>
void DLList<Object>::push_back(const Object &x) {
    insert(end(), x);
}
```
* Este es el metodo push_back de la clase DLList que inserta un nuevo elemento al final de la lista doblemente enlazada con
el valor propocionado
```c++
template<typename Object>
void DLList<Object>::push_back(Object &&x) {
    insert(end(), std::move(x));
}
```
* Este es el metodo push_back de la clase DLList que inserta un nuevo elemento al final de la lista doblemente enlazada utilizando
una referencia de movimiento.
```c++
template<typename Object>
void DLList<Object>::pop_front() {
    erase(begin());
}
```
* Este es el metodo pop_front de la clase DLList que elimina el primer elemento de la lista doblemente enlazada.
```c++
template<typename Object>
void DLList<Object>::pop_back() {
    erase(--end());
}
```
* Este es el metodo pop_back de la clase DLList que elimina el ultimo elemento de la lista doblemente enlazada
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, const Object &x) {
    Node *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new Node{x, p->prev, p}};
}
```
* Este es el metodo insert() de la clase DLList que inserta un nuevo elemento antes de la posicion indicada por el iterador pasado como argumento.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::insert(iterator itr, Object &&x) {
    Node *p = itr.current;
    theSize++;
    return {p->prev = p->prev->next = new Node{std::move(x), p->prev, p}};
}
```
* Este es el metodo insert de la clase DLList que inserta un nuevo elemento antes de la posicion indicada por el iterador pasado como argumento
utilizando una referencia de movimiento.
```c++
template<typename Object>
void DLList<Object>::insert(int pos, const Object &x) {
    insert(get_iterator(pos), x);
}
```
* Este es el metodo inser de la clase DLList que inserta un nuevo elemento en la posicion indicada por pos con el valor x
```c++
template<typename Object>
void DLList<Object>::insert(int pos, Object &&x) {
    insert(get_iterator(pos), std::move(x));
}
```
* Este es el metodo insert de la clase DLList que inserta un nuevo elemento en la posicion indicada por pos utilizando una referencia de movimiento.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator itr) {
    Node *p = itr.current;
    iterator retVal(p->next);
    p->prev->next = p->next;
    p->next->prev = p->prev;
    delete p;
    theSize--;
    return retVal;
}
```
* Este es el metodo erase de la clase DLList, que elimina el elemento apuntado por el iterador de la lista doblemente enlazada.
```c++
template<typename Object>
void DLList<Object>::erase(int pos) {
    erase(get_iterator(pos));
}
```
* Esto es el metodo erase de la clase DLList que elimina el elemento en la posicion indicada por pos.
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::erase(iterator from, iterator to) {
    for(iterator itr = from; itr != to;) {
        itr = erase(itr); // Llama al método erase() para eliminar el elemento apuntado por itr y obtiene el iterador al siguiente elemento
    }
    return to; // Retorna el iterador 'to', que marca el final del rango después de eliminar los elementos
}
```
Este es el metodo erase de la clase DLList que elimina los elemento del rango especificado por los iteradores from y to.
```c++
template<typename Object>
void DLList<Object>::print() const {
    for(const auto &item : *this) { // Itera sobre todos los elementos de la lista utilizando un bucle for-each
        std::cout << item << " "; // Imprime cada elemento seguido de un espacio en blanco
    }
    std::cout << std::endl; // Imprime una nueva línea al final
}
```
* Este es el metodo print que imprime todos los elementos almacenados en la lista
```c++
template<typename Object>
void DLList<Object>::init() {
    theSize = 0;
    head = new Node;
    tail = new Node;
    head->next = tail;
    tail->prev = head;
}
```
* Este es el metodo init() de la calse DLList que inicializa la lista estableciendo el tamaño a 0 y creando nodos de cabeza y cola
```c++
template<typename Object>
typename DLList<Object>::iterator DLList<Object>::get_iterator(int pos) {
    iterator itr = begin();
    for(int i = 0; i < pos; ++i) {
        ++itr;
    }
    return itr;
}
```
* Este es el metodo get_iterator de la clase DLList que devuelve un iterador que apunta al elemento en la posicion especificada por pos.