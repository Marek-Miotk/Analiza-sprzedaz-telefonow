>> Opis projektu

Projekt ten ma na celu przeprowadzenie szczegółowej analizy danych sprzedaży telefonów z pliku Sales.csv. Analiza koncentruje się na zbadaniu wyników sprzedaży różnych marek telefonów, analizie przychodów, rabatów, rozkładzie cen, a także na korelacji między rozmiarem pamięci a ceną telefonu. Wszystkie analizy zostały przeprowadzone przy użyciu Pythona i bibliotek takich jak Pandas, Matplotlib, Seaborn.

>> Dane

Dane zawierają informacje o sprzedaży telefonów różnych marek. Główne kolumny w danych to:

    Brands: Marka telefonu
    Models: Model telefonu
    Selling Price: Cena sprzedaży telefonu
    Discount: Rabat przyznany na dany telefon
    Storage: Rozmiar pamięci telefonu (np. 64GB, 128GB)

>> Zastosowane narzędzia

    Python (Jupyter)
    Pandas – do przetwarzania danych
    Matplotlib – do tworzenia wykresów
    Seaborn – do wizualizacji danych

>> Kroki analizy

    - Wczytanie danych: Dane zostały załadowane z pliku Sales.csv za pomocą Pandas.
    - Analiza sprzedaży: Zidentyfikowanie, która marka sprzedała najwięcej telefonów.
    - Rozkład sprzedaży modeli: Zbadanie, jak rozkładała się sprzedaż poszczególnych modeli w obrębie danej marki.
    - Przychody: Obliczenie, ile dana marka zarobiła łącznie oraz na poszczególnych modelach.
    - Rabaty: Obliczenie, ile rabatów przyznała dana marka oraz na poszczególnych modelach.
    - Średnia cena sprzedaży: Obliczenie średniej ceny sprzedaży telefonu oraz mediany ceny w obrębie każdej marki. Agregacja danych - tabela.
    - Analiza pamięci: Zbadanie, jak rozkładała się sprzedaż telefonów o różnych rozmiarach pamięci w obrębie różnych marek.
    - Korelacja między pamięcią a ceną: Sprawdzenie, czy istnieje zależność między rozmiarem pamięci a ceną telefonu.

----------------------------------------------------------

>> Kroki analizy w kodzie

    1. Analiza sprzedaży telefonów wg marki
      
    df.value_counts("Brands")

    Analizuje, która marka sprzedała najwięcej telefonów.
    
    2. Analiza sprzedaży modeli w obrębie danej marki
    
    Samsung = df.loc[(df["Brands"] == "SAMSUNG")]
    Samsung[["Brands", "Models"]].value_counts()
    
    Sprawdza rozkład sprzedaży modeli dla wybranej marki (np. Samsung, Apple).

    df["Licznik"] = 0
    df.groupby(["Brands", "Models"]).count()["Licznik"]
    
    Przedstawia zagregowane dane dla wszystkich marek
  
    3. Przychody marek

    Przychody_marek = df.groupby("Brands")["Selling Price"].sum()

    Oblicza łączne przychody dla każdej marki.

    4. Przychody marek dla każdego modelu
    
    Przychod_modele = df.groupby(["Brands", "Models"])["Selling Price"].sum()

    Oblicza przychody ze sprzedazy dla każdego modelu i dla każdej marki.
  
    5. Rabaty przyznane przez marki

    Rabaty_lacznie = df.groupby(["Brands"])["Discount"].sum()

    Oblicza łączną wartość rabatów przyznanych przez każdą markę.
    
    6. Rabaty przyznane przez marki dla każdego modelu

    Rabaty_modele = df.groupby(["Brands", "Models"])["Discount"].sum()

    Oblicza łączną wartość rabatów przyznanych przez każdą markę dla każdego modelu.
    
    7. Średnia cena telefonu w obrębie danej marki

    sredni_przychod_modele = (df.groupby(["Brands", "Models"])["Selling Price"].mean()).round(2)

    Oblicza średnią cenę sprzedaży telefonu dla każdej marki.
    
    8. Średni rabat przyznany przez markę dla każdego telefonu

    sredni_rabat_modele = (df.groupby(["Brands", "Models"])["Discount"].mean()).round(2)

    Oblicza średni rabat przyznany przez markę dla każdego telefonu.
    
    9. Korelacja między rozmiarem pamięci a ceną telefonu

    def konwersja_na_GB(pamiec)
    df2["Storage_GB"] = df2["Storage"].apply(konwersja_na_GB)
    kor_pamiec_cena = sns.lmplot(x = "Storage_GB", y = "Selling Price", hue = "Brands", data = df2)

    Dostosowuje jednostki pamięci ( MB, GB, TB) do wspólnej GB. Analizuje korelację między rozmiarem pamięci a ceną telefonu. Tworzy wykres zależności.
    
>> Wizualizacje

W projekcie zostały wykorzystane różne wykresy do wizualizacji wyników analizy:

    * Tabela zestawieniowa z danymi zagregowanymi dotyczacymi przychodów i rabatów (sumy, średnie, mediany).
    * Wykresy słupkowe – do przedstawienia rozkładu telefonów według rozmiaru pamięci.
    * Wykresy liniowe – do przedstawienia korelacji między pamięcią a ceną telefonu.

>> Przykładowe wyniki

1. Największa sprzedaż wg marki:
    * Samsung:   719 szt.
    * Apple      387 szt.
      
2. Średnia cena sprzedaży telefonu w obrębie marki:
    * Samsung:   24296.25 [j]
    * Apple:     81985.56 [j]
      
3. Średni rabat przyznany przez markę:
    * Samsung:   10.44%
    * Apple:     3.58%
