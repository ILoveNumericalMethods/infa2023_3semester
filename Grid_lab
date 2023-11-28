#include <iostream>
#include <stdexcept>
#include <cassert>

typedef unsigned long long ull;
using namespace std;

template <typename T, int N>
class Grid final {
private:
    unsigned int dimention = N;
    T* data = nullptr;
    ull * size = nullptr;
    
public:

    Grid() {};

    Grid(Grid<T, N> const& other) //конструктор копирования
    { 
        dimention = other.dimention;
        size = new ull[N];
        unsigned long long data_size = 1;
        for (int i = 0; i < dimention; i++)
        {
            size[i] = other.size[i];
            data_size *= size[i];
        }

        data = new T[data_size];

        for (int i = 0; i < data_size; i++)
        {
            data[i] = other.data[i];
        }
    }

    Grid<T, N>& operator=(Grid<T, N> const& other) //оператор копирования
    { 
        size = new ull[N];
        for (int i = 0; i < other.dimention; i++)
        {
            if (size[i] != other.size[i])
            {
                throw exception("invalid grid size");
                return *this;
            }
        }

        ull data_size = 1;
        for (int i = 0; i < dimention; i++)
        {
            size[i] = other.size[i];
            data_size *= size[i];
        }

        for (int i = 0; i < data_size; i++)
        {
            data[i] = other.data[i];
        }

        return *this;
    }

    Grid(Grid<T, N>&& other) // конструктор перемещением
    {
        size = other.size;
        data = other.data;

        other.data = nullptr;
        other.size = nullptr;
    }

    Grid<T, N>& operator=(Grid<T, N>&& other) // оператор пермещения
    {
        data = other.data;
        size = other.size;

        other.data = nullptr;
        other.size = nullptr;

        return *this;
    }

    ~Grid() // деструктор
    {
        delete[] data;
        delete[] size;
    }

    Grid(T const& t) // контруктор едиственного узла
    {
        size = new ull[N];
        for (int i = 0; i < dimention; i++)
        {
            size[i] = 1;
        }

        data = new T[1];

        data[0] = t;
    }

    Grid(ull* const new_size, T* const new_data) // конструктор через массивы
    {
        size = new ull[N];
        for (int i = 0; i < dimention; i++)
        {
            size[i] = new_size[i];
        }

        ull data_size = 1;
        for (int i = 0; i < dimention; i++)
        {
            data_size *= size[i];
        }

        data = new T[data_size];

        for (int i = 0; i < data_size; i++)
        {
            data[i] = new_data[i];
        }
    }

    // далее идет кусок кода который не работает и я не знаю почему :(
    // по идее функция configure_size должна быть в private но она все равно не работает

/*
    template<typename ... Args>
    void configure_size(int i, ull first, Args ... args)
    {
        if (i == N)
        {
            return;
        }

        size[i] = first;
        configure_size(i + 1, args...);
    }

    template<typename... Args>
    Grid(T t, Args... args)
    {
        size = new ull[N];
        configure_size<Args>(0, args...);

        ull data_size = 1;
        for(int i = 0 ; i < n; i++)
        {
            data_size *= size[i];
        }
        
        data = new T[data_size];
        for (int i = 0; i < data_size; i++)
        {
            data[i] = t;
        }
    }

*/
    Grid<T, N - 1> operator[](ull index) // оператор уменьшения размерности сетки
    {
        ull* new_size = new ull[dimention - 1];
        for (int i = 0; i < N - 1; i++)
        {
            new_size[i] = size[i + 1];
        }

        ull new_data_size = 1;
        for (int i = 0; i < dimention - 1; i++)
        {
            new_data_size *= new_size[i];
        }

        T* new_data = new T[new_data_size];
        for (int i = 0; i < new_data_size; i++)
        {
            new_data[i] = data[index * new_data_size + i];
        }

        Grid<T, N - 1> new_grid(new_size, new_data);

        delete[] new_size;
        delete[] new_data;

        return new_grid;
    }

    T& operator () (ull index = 0) // опертатор обращенния по индексу
    {
        return data[index];
    }
};


int main()
{
    return 0;
}
