# Navigation Drawer avec Fragments en Java – Android Studio

## Introduction

Ce projet montre comment créer une application Android utilisant un Navigation Drawer avec plusieurs Fragments en Java.

Fonctionnalités :
- Menu latéral (Navigation Drawer)
- Affichage dynamique des Fragments
- Utilisation d’un ListFragment
- Icônes personnalisées
- Gestion des fragments avec FragmentManager

---

# Étape 1 – Création du projet

## Créer un nouveau projet Android

1. Ouvrir Android Studio
2. Cliquer sur :

text
New Project


3. Choisir :

text
Navigation Drawer Activity


4. Configuration :
- Langage : Java
- Min SDK : 24
- Nom : NavigationDrawerDemo

---

## Ce que génère automatiquement Android Studio

Le template crée :
- MainActivity.java
- activity_main_drawer.xml
- nav_header_main.xml
- content_main.xml

---

# Étape 2 – Modifier le menu du Navigation Drawer

## Fichier :

text
res/menu/activity_main_drawer.xml


## Remplacer le contenu par :

xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/nav_fragment1"
        android:icon="@drawable/ic_home"
        android:title="Fragment 1" />

    <item
        android:id="@+id/nav_fragment2"
        android:icon="@drawable/ic_dashboard"
        android:title="Fragment 2" />

    <item
        android:id="@+id/nav_list"
        android:icon="@drawable/ic_list"
        android:title="Fragment List" />

</menu>


---

# Étape 3 – Ajouter des icônes

## Créer les Vector Assets

Chemin :

text
res/drawable
→ clic droit
→ New
→ Vector Asset


---

## Choisir des icônes Clip Art

Créer :
- ic_home.xml
- ic_dashboard.xml
- ic_list.xml

---

# Étape 4 – Créer les Fragments

## Créer BlankFragment

Chemin :

text
File
→ New
→ Fragment
→ Fragment (Blank)


Nom :

text
BlankFragment


Décocher :
- Include fragment factory methods
- Include interface callbacks

---

## Créer BlankFragment2

Même procédure :

text
BlankFragment2


---

# Étape 5 – Modifier le layout des fragments

## fragment_blank.xml

xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical"
    android:background="#F8BBD0">

    <TextView
        android:text="Fragment 1"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#000"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</LinearLayout>


---

## fragment_blank2.xml

xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical"
    android:background="#3F51B5">

    <TextView
        android:text="Fragment 2"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="#FFF"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

</LinearLayout>


---

# Étape 6 – Ajouter le conteneur des fragments

## Ouvrir :

text
res/layout/content_main.xml


## Ajouter :

xml
<FrameLayout
    android:id="@+id/contenu"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />


---

# Étape 7 – Gérer les clics du menu

## Modifier MainActivity.java

Ajouter la méthode :

java
@Override
public boolean onNavigationItemSelected(@NonNull MenuItem item) {

    int id = item.getItemId();

    if (id == R.id.nav_fragment1) {

        getSupportFragmentManager()
                .beginTransaction()
                .replace(R.id.contenu, new BlankFragment())
                .commit();

    } else if (id == R.id.nav_fragment2) {

        getSupportFragmentManager()
                .beginTransaction()
                .replace(R.id.contenu, new BlankFragment2())
                .commit();

    } else if (id == R.id.nav_list) {

        getSupportFragmentManager()
                .beginTransaction()
                .replace(R.id.contenu, new FragmentList())
                .commit();
    }

    DrawerLayout drawer = findViewById(R.id.drawer_layout);
    drawer.closeDrawer(GravityCompat.START);

    return true;
}


---

# Explication du code

## FragmentManager

java
getSupportFragmentManager()


Permet de gérer les fragments.

---

## beginTransaction()

Démarre une transaction de fragments.

---

## replace()

java
.replace(R.id.contenu, new BlankFragment())


Remplace le fragment affiché dans le FrameLayout.

---

## commit()

Valide la transaction.

---

## closeDrawer()

Ferme le menu latéral après le clic.

---

# Étape 8 – Créer un ListFragment

## Créer FragmentList.java

java
package com.example.navigationdrawer;

import android.os.Bundle;
import android.widget.ArrayAdapter;

import androidx.fragment.app.ListFragment;

public class FragmentList extends ListFragment {

    @Override
    public void onActivityCreated(Bundle savedInstanceState) {

        super.onActivityCreated(savedInstanceState);

        String[] items = {
                "Item 1",
                "Item 2",
                "Item 3",
                "Item 4",
                "Item 5",
                "Item 6",
                "Item 7",
                "Item 8",
                "Item 9",
                "Item 10"
        };

        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                getActivity(),
                android.R.layout.simple_list_item_1,
                items
        );

        setListAdapter(adapter);
    }
}


---

# Fonctionnement du ListFragment

## ArrayAdapter

java
ArrayAdapter<String>


Permet d’afficher une liste de chaînes de caractères.

---

## setListAdapter()

Associe l’adapter au ListFragment.

---

# Étape 9 – Exécuter l’application

## Lancer l’émulateur

Puis :

text
Run > Run app


---

# Résultat attendu

## Fragment 1
- Fond rose
- Texte : Fragment 1

---

## Fragment 2
- Fond bleu
- Texte : Fragment 2

---

## Fragment List
- Liste des éléments Item 1 → Item 10

---

# Structure du projet

text
NavigationDrawerDemo/
│
├── java/
│   ├── MainActivity.java
│   ├── BlankFragment.java
│   ├── BlankFragment2.java
│   └── FragmentList.java
│
├── res/
│   ├── layout/
│   │   ├── activity_main.xml
│   │   ├── content_main.xml
│   │   ├── fragment_blank.xml
│   │   └── fragment_blank2.xml
│   │
│   ├── menu/
│   │   └── activity_main_drawer.xml
│   │
│   └── drawable/
│       ├── ic_home.xml
│       ├── ic_dashboard.xml
│       └── ic_list.xml
│
└── AndroidManifest.xml


---

# Concepts utilisés

| Concept | Description |
|---|---|
| Navigation Drawer | Menu latéral Android |
| Fragment | Interface réutilisable |
| FragmentManager | Gestion des fragments |
| FrameLayout | Conteneur dynamique |
| ListFragment | Fragment avec liste |
| ArrayAdapter | Adaptateur de données |

---

# Conclusion

Cette application permet :
- D’utiliser un Navigation Drawer Android
- D’afficher plusieurs fragments dynamiquement
- De manipuler FragmentManager
- D’utiliser ListFragment et ArrayAdapter
- De structurer une application Android moderne en Java
