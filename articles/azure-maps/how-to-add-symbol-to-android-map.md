---
title: Ajouter une couche de symboles à des cartes Android | Microsoft Azure Maps
description: Découvrez comment ajouter un marqueur à une carte. Consultez un exemple qui utilise l’Android SDK Azure Maps pour ajouter une couche de symboles qui contient des données basées sur des points à partir d’une source de données.
author: anastasia-ms
ms.author: v-stharr
ms.date: 04/26/2019
ms.topic: how-to
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.openlocfilehash: 10969e20cd7ae71cade230f6643a27d5d940ceaa
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91311272"
---
# <a name="add-a-symbol-layer-to-a-map-using-azure-maps-android-sdk"></a>Ajouter une couche de symboles à une carte à l’aide de l’Android SDK Azure Maps

Cet article montre comment restituer des données de points à partir d’une source de données sous la forme d’une couche de symboles sur une carte à l’aide de l’Android SDK Azure Maps.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez installer l’[Android SDK Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-use-android-map-control-library) afin de charger une carte.

## <a name="add-a-symbol-layer"></a>Ajouter un calque de symboles

Pour ajouter un repère sur la carte à l’aide de la couche de symboles, procédez comme suit :

1. Modifiez le fichier **res** > **layout** > **activity_main.xml** afin qu’il ressemble au code XML suivant :
    
    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >

        <com.microsoft.azure.maps.mapcontrol.MapControl
            android:id="@+id/mapcontrol"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:mapcontrol_centerLat="47.64"
            app:mapcontrol_centerLng="-122.33"
            app:mapcontrol_zoom="12"
            />

    </FrameLayout>
    ```

2. Copiez l’extrait de code suivant dans la méthode **onCreate()** de votre classe `MainActivity.java`.

    ```Java
    mapControl.onReady(map -> {
    
        //Create a data source and add it to the map.
        DataSource dataSource = new DataSource();
        map.sources.add(dataSource);
    
        //Create a point feature and add it to the data source.
        dataSource.add(Feature.fromGeometry(Point.fromLngLat(-122.33, 47.64)));
    
        //Add a custom image icon to the map resources.
        map.images.add("my-icon", R.drawable.mapcontrol_marker_red);
    
        //Create a symbol layer and add it to the map.
        map.layers.add(new SymbolLayer(dataSource,
            iconImage("my-icon")));
        });
    
    ```
    
    L’extrait de code ci-dessus commence par obtenir une instance de contrôle de carte Azure Maps en utilisant la méthode de rappel **onReady()** . Il crée ensuite un objet source de données à l’aide de la classe **DataSource**, puis l’ajoute à la carte. Puis il y ajoute une **fonctionnalité** contenant une géométrie de point. Une image de repère rouge est définie comme icône pour le symbole. Une **couche de symboles** utilise du texte ou des icônes pour restituer des données basées sur des point qui sont encapsulées dans la source de données en tant que symboles sur la carte. Une couche de symboles est créée à laquelle la source de données est transmise à des fins de restitution, qui vient s’ajouter aux couches de la carte.
    
    Après avoir ajouté l’extrait de code ci-dessus, votre `MainActivity.java` devrait ressembler à celui ci-dessous :
    
    ```Java
    package com.example.myapplication;
    
    import android.app.Activity;
    import android.os.Bundle;
    import com.mapbox.geojson.Feature;
    import com.mapbox.geojson.Point;
    import com.microsoft.azure.maps.mapcontrol.AzureMaps;
    import com.microsoft.azure.maps.mapcontrol.MapControl;
    import com.microsoft.azure.maps.mapcontrol.layer.SymbolLayer;
    import com.microsoft.azure.maps.mapcontrol.source.DataSource;
    import static com.microsoft.azure.maps.mapcontrol.options.SymbolLayerOptions.iconImage;
    public class MainActivity extends AppCompatActivity {
        
        static{
                AzureMaps.setSubscriptionKey("<Your Azure Maps subscription key>");
            }
    
        MapControl mapControl;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
    
            mapControl = findViewById(R.id.mapcontrol);
    
            mapControl.onCreate(savedInstanceState);
    
            mapControl.onReady(map -> {
    
                //Create a data source and add it to the map.
                DataSource dataSource = new DataSource();
                map.sources.add(dataSource);
            
                //Create a point feature and add it to the data source.
                dataSource.add(Feature.fromGeometry(Point.fromLngLat(-122.33, 47.64)));
            
                //Add a custom image icon to the map resources.
                map.images.add("my-icon", R.drawable.mapcontrol_marker_red);
            
                //Create a symbol layer and add it to the map.
                map.layers.add(new SymbolLayer(dataSource,
                    iconImage("my-icon")));
            });
        }
    
        @Override
        public void onStart() {
            super.onStart();
            mapControl.onStart();
        }
    
        @Override
        public void onResume() {
            super.onResume();
            mapControl.onResume();
        }
    
        @Override
        public void onPause() {
            super.onPause();
            mapControl.onPause();
        }
    
        @Override
        public void onStop() {
            super.onStop();
            mapControl.onStop();
        }
    
        @Override
        public void onLowMemory() {
            super.onLowMemory();
            mapControl.onLowMemory();
        }
    
        @Override
        protected void onDestroy() {
            super.onDestroy();
            mapControl.onDestroy();
        }
    
        @Override
        protected void onSaveInstanceState(Bundle outState) {
            super.onSaveInstanceState(outState);
            mapControl.onSaveInstanceState(outState);
        }
    }
    ```
    
À ce stade, si vous exécutez votre application, vous devriez voir un repère sur la carte, comme illustré ici :

<center>

![Épingle sur une carte Android](./media/how-to-add-symbol-to-android-map/android-map-pin.png)</center>

> [!TIP]
> Par défaut, les couches de symboles optimisent l’affichage des symboles en masquant ceux qui se chevauchent. Quand vous effectuez un zoom avant, les symboles masqués deviennent visibles. Pour désactiver cette fonctionnalité et afficher tous les symboles en permanence, affectez à l’option `iconAllowOverlap` la valeur `true`.

## <a name="next-steps"></a>Étapes suivantes

Pour ajouter des éléments à votre carte, voir :

> [!div class="nextstepaction"]
> [Ajouter des formes à une carte Android](https://docs.microsoft.com/azure/azure-maps/how-to-add-shapes-to-android-map)

> [!div class="nextstepaction"]
> [Afficher des informations sur les caractéristiques](display-feature-information-android.md)