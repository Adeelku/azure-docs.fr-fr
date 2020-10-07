---
title: 'Démarrage rapide : Se connecter à l’aide de PHP – Azure Database pour MySQL'
description: Ce guide de démarrage rapide fournit plusieurs exemples de code PHP, que vous pouvez utiliser pour vous connecter et interroger des données de la base de données Azure pour MySQL.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 5/26/2020
ms.openlocfilehash: 9b05149515f2d40ad8043cd65c2ec5589440713e
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/05/2020
ms.locfileid: "90882526"
---
# <a name="quickstart-use-php-to-connect-and-query-data-in-azure-database-for-mysql"></a>Démarrage rapide : Utilisation de PHP pour se connecter et interroger des données dans Azure Database pour MySQL
Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL en utilisant une application [PHP](https://secure.php.net/manual/intro-whatis.php). Il détaille l’utilisation d’instructions SQL pour interroger la base de données, la mettre à jour, y insérer des données ou en supprimer. Cette rubrique part du principe que vous connaissez les bases du développement à l’aide de PHP et que vous ne savez pas utiliser Azure Database pour MySQL.

## <a name="prerequisites"></a>Prérequis
Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :
- [Créer un serveur de base de données Azure pour MySQL à l’aide du Portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

> [!IMPORTANT] 
> Vérifiez que l’adresse IP à partir de laquelle vous vous connectez a été ajoutée aux règles de pare-feu du serveur à l’aide du [portail Azure](./howto-manage-firewall-using-portal.md) ou [d’Azure CLI](./howto-manage-firewall-using-cli.md)

## <a name="install-php"></a>Installer PHP
Installez PHP sur votre serveur, ou créez une [application web](../app-service/overview.md) Azure incluant PHP.

### <a name="macos"></a>MacOS
- Téléchargez [PHP version 7.1.4](https://secure.php.net/downloads.php).
- Installez PHP et consultez le [manuel PHP](https://secure.php.net/manual/install.macosx.php) pour poursuivre la configuration.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](https://secure.php.net/downloads.php).
- Installez PHP et consultez le [manuel PHP](https://secure.php.net/manual/install.unix.php) pour poursuivre la configuration.

### <a name="windows"></a>Windows
- Téléchargez [la version non thread-safe de PHP 7.1.4 (x64)](https://windows.php.net/download#php-7.1).
- Installez PHP et consultez le [manuel PHP](https://secure.php.net/manual/install.windows.php) pour poursuivre la configuration.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL. Vous devez disposer du nom de serveur complet et des informations d’identification.

1. Connectez-vous au [portail Azure](https://portal.azure.com/).
2. Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **mydemoserver**.
3. Cliquez sur le nom du serveur.
4. Dans le panneau **Vue d’ensemble** du serveur, notez le **nom du serveur** et le **nom de connexion de l’administrateur du serveur**. Si vous oubliez votre mot de passe, vous pouvez également le réinitialiser dans ce panneau.
 :::image type="content" source="./media/connect-php/1_server-overview-name-login.png" alt-text="Nom du serveur de base de données Azure pour MySQL":::

## <a name="connect-and-create-a-table"></a>Se connecter et créer une table
Utilisez le code suivant pour vous connecter et créer une table à l’aide de l’instruction SQL **CREATE TABLE**. 

Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP. Il appelle les méthodes [mysqli_init](https://secure.php.net/manual/mysqli.init.php) et [mysqli_real_connect](https://secure.php.net/manual/mysqli.real-connect.php) pour se connecter à MySQL. Ensuite, il appelle la méthode [mysqli_query](https://secure.php.net/manual/mysqli.query.php) pour exécuter la requête. Enfin, il appelle la méthode [mysqli_close](https://secure.php.net/manual/mysqli.close.php) pour fermer la connexion.

Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs. 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

// Run the create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Insertion des données
Utilisez le code suivant pour vous connecter et insérer des données à l’aide d’une instruction SQL **INSERT**.

Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP. Le code utilise la méthode [mysqli_prepare](https://secure.php.net/manual/mysqli.prepare.php) pour créer une instruction Insert préparée, puis lie les paramètres de chaque valeur de colonne insérée à l’aide de la méthode [mysqli_stmt_bind_param](https://secure.php.net/manual/mysqli-stmt.bind-param.php). Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](https://secure.php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](https://secure.php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs. 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close the connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Lire les données
Utilisez le code suivant pour vous connecter et lire des données à l’aide d’une instruction SQL **SELECT**.  Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP. Le code utilise la méthode [mysqli_query](https://secure.php.net/manual/mysqli.query.php) pour exécuter la requête sql, et la méthode [mysqli_fetch_assoc](https://secure.php.net/manual/mysqli-result.fetch-assoc.php) pour extraire les lignes ainsi créées.

Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs. 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Mettre à jour des données
Utilisez le code suivant pour vous connecter et mettre à jour les données à l’aide d’une instruction SQL **UPDATE**.

Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP. Le code utilise la méthode [mysqli_prepare](https://secure.php.net/manual/mysqli.prepare.php) pour créer une instruction Update préparée, puis lie les paramètres de chaque valeur de colonne mise à jour à l’aide de la méthode [mysqli_stmt_bind_param](https://secure.php.net/manual/mysqli-stmt.bind-param.php). Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](https://secure.php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](https://secure.php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs. 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close the connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Suppression de données
Utilisez le code suivant pour vous connecter et lire les données à l’aide d’une instruction SQL **DELETE**. 

Ce code utilise la classe **d’extension MySQL améliorée** (mysqli) incluse dans PHP. Le code utilise la méthode [mysqli_prepare](https://secure.php.net/manual/mysqli.prepare.php) pour créer une instruction Delete préparée, puis lie les paramètres de la clause Where à l’aide de la méthode [mysqli_stmt_bind_param](https://secure.php.net/manual/mysqli-stmt.bind-param.php). Il exécute l’instruction à l’aide de la méthode [mysqli_stmt_execute](https://secure.php.net/manual/mysqli-stmt.execute.php), puis ferme l’instruction à l’aide de la méthode [mysqli_stmt_close](https://secure.php.net/manual/mysqli-stmt.close.php).

Remplacez les paramètres db_name, de l’hôte, du nom d’utilisateur et du mot de passe par vos propres valeurs. 

```php
<?php
$host = 'mydemoserver.mysql.database.azure.com';
$username = 'myadmin@mydemoserver';
$password = 'your_password';
$db_name = 'your_database';

//Establishes the connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}

//Run the Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close the connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Se connecter à Azure Database pour MySQL via SSL](howto-configure-ssl.md)
