#include <iostream>
#include<algorithm>
#include<fstream>

using namespace std;

int suma, i, j, rozmiar;

//malejaco
bool porownaj(int a, int b)
{
    return a>b;
}



int *tworzenie() //tworzymy i wypelniamy tablice
{
    cout << "Podaj rozmiar tablicy: ";
    cin >> rozmiar;

    while(cin.fail() || rozmiar <= 1) //sprawdzamy poprawnosc wpisywanych danych
    {
        cout << "Niepoprawna wartosc" << endl;
        cin.clear();
        cin.ignore(50,'\n');
        cin >> rozmiar;

    }

    int* tab = new int[rozmiar]; //tablica dynamiczna o rozmiarze rozmiar

    for(int i = 0; i < rozmiar; i++) //użytkownik uzupelnia dane
    {
        cout << "Podaj "<<i+1<<" element tablicy" <<endl;
        cin >> tab[i];
       while(cin.fail()) //sprawdzamy poprawnosc wpisywanych danych
       {
           cout << "Zla wartosc, wprowadz liczbe!"<<endl;
           cin.clear();
           cin.ignore(50, '\n');
           cin >> tab[i];
       }


    }

 sort(tab, tab + rozmiar, porownaj); //sortujemy tablice w kolejnosci malejacej

  suma = 0;
  for(int i=0;i<rozmiar;i++)
        suma=tab[i]+suma;


    return tab;

}


void podZbior(int tab[]) //zadanie
{

    ofstream wynik("wynik.txt");

    int pom = tab[0]; // funkcja pomocnicza, przypisujemy jej najwiekszą wartośc z tablicy
    while (pom<suma && j<rozmiar && pom!=suma-pom ) //sprawdzamy czy tablica spelnia warunki zadania
   {
       if(pom > suma-pom) //warunek zostaje spelniony
       {

           cout << "Najmniejszy podzbior sklada sie z "<<j+1<<" element/ow: ";

           cout << "["<<tab[0];
           wynik<<tab[0];
           for (i=1;i<=j;i++)
           {
               cout << ", "<< tab[i];
               wynik<<", "<<tab[i] ; //wypisanie wyniku do pliku
           }
           cout << "]";
               wynik.close();
            goto poprawnie;
       }

     else
        {
            pom = pom+tab[i];
            j++;
        }

    }

        cout <<"Brak podzbiorow spelniajacych zadane kryteria";


poprawnie:
 cout<<endl;
 cout<<"Koniec zadania"<<endl;
}



int main()
{


    int* tablica = tworzenie();
    podZbior(tablica);
    delete [] tablica;

    return 0;
}
