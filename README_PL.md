+ [Wersja angielska - EN](https://www.apisql.com/)

# [APIsql](https://www.apisql.com)

![apisql-logo.png](https://logo.apiexec.com/apisql-logo.png)

https://github.com/apisql


Projekt apisql jest wspierany przez [API Foundation](https://apifoundation.com)

## Rozwiązania wspierane przez [API Foundation](https://apifoundation.com)

Od początku działania (w 2018 roku) tworzyliśmy kilka koncepcji skupionych wokół jednej idei: szybszego wytwarzania orogramowania
Obecnie w roku 2020 oferujemy rozwiązania:

+ [APIexec - executor, aplikacja uruchamiająca skrypty powłoki shell](https://www.apiexec.com)
+ [APIcra - biblioteki skryptów shell](https://www.apicra.com)
+ [APIunit - definicje aplikacji oraz środowiska dla ciągłej kontroli wytwarzania oprogramowania](https://www.apiunit.com)
+ [APIbuild - monitorowanie wytwarzania oprogramowania, jakość i wersjonowanie ](https://www.apibuild.com)
+ [APIsql - bazy danych, zapytania, modele](https://www.apisql.com)
+ [APIfunc - rozwiązania dla FaaS](https://www.apifunc.com)

## About APIexec

APIexec it's a runner for bash scripts, written in many programming languages as a library:
+ nodejs
+ php
+ python

## Is using in projects:
+ [APIcra](https://www.apicra.com)
+ [ProMaGen](https://www.promagen.com/)
+ [DevOpsTerminal](https://docs.devopsterminal.com/)


## Witamy na stronie projektu APIsql

Celem jest stworzenie warunków do jak najszybszej migracji aplikacji pomiędzy:
+ wersjami
+ architekturami
+ privderami środowiska


Dane oprócz kodu aplikacji są istotnym często implementowaną częścią aplikacji
która jest implementowana w zalezności od zastosowanego rozwiązania.

Bazą często jest język komunikacji bazy danych: SQL

warto wobec tego wykorzystać już utworzony kod lub generowany poprzez PDo i komunikować się z bazą danych
mimo innych warunków zewnętrzynch jak: zmiana bazy danych czy mikrousługowa architektura.

## Existing solutions
https://cloud-elements.com/elements/sql-server-api/

One-to-Many
One API Integration to connect you to all the leading database services: MySQL, SQL Server and PostreSQL.
HubSpot API


Simple Data Mapping
Using Element Mapper, our drag-and-drop UI, easily map and normalize data objects and fields between leading cloud services.
Marketing Cloud Services


Stay Up to Date
We even manage user access and authentication, API updates, logging and monitoring, all from a consistent platform.

## Make Api fast
https://nordicapis.com/making-fast-apis-lessons-learned-from-40-years-of-sql/


## Another
https://carto.com/developers/sql-api/reference/#operation/postSQLStatement


## Why apiSQL
This is tool, which is the first step to reach in practical some parts of goals for UnitApi which will be later the main standard to build any API

urlQuery -> sqlQuery

# apiSQL
This tools is able to create meta data from SQL statement and SQL schema
The way from SQL to API is possbile with one step, just for configuration


## import-export generator
apisql.yaml


    version: 1.1.0
      name: Import data from localhost application  
      import:
        file:
        dump:
        db:
          host:
          password          
      export:
        file:


## Input
The sql file


## Output
The Code, sdk


## Parsing, Structure of schema

    Source
        Collection
            Object
                Param

    Collection
        List: 1,2,9,11
        Range: 1-11, A-M 
        Filter:
            Object,Param

    Object:
        Create
        Read
        Update
        Delete

    Param
        Get
        Set


### output: collection | CRUD
many items
Collection as model,view (one or more models)

    Schema:
        source-output-model-command

    Path:
        {source}/{output}/{model}/{command}    


    Condition:
        where: id/1/2/3/4/5
        between: id/10/20
        where: name/to
    
    Command
        Create - json can many create
        read - can many list
            Filter - json
            Range - json
            Param: -list of param - Which attributes show

#### Example:

    db/collection/user/read - json
    db/collection/user/delete - json
    db/collection/user/update - json
    db/collection/user/create - json    


### output: model | RUD
one item

    Schema:
        source-output-model-method-command-param-value

    Path:
        {source}/{output}/{model}/{command}/{condition}/{param}/{value}/

    Condition:
        where
    
    Command:
        ReadBy
        UpdateBy -json
        DeleteBy

#### Example:

    db/model/user/ReadBy/id/10
    db/model/user/DeleteBy/login/tom


### output: param | RU
one param from one item

    Schema:
        source-output-model-param-param-value

    Path:
        {source}/{output}/{model}/{param}/{command}/{condition}/{param}/{value}/

    Condition:
        where
    
    Command:
        Get - Read
        Set - Update

#### Example:

    db/param/user/login/Read/id/10
    db/param/user/password/read/where/login/tom
    db/param/user/login/update/where/login/tom


### Routing, Example

    Model: User
    Structure:
    User:
        id
        login
        password
        created_at

#### Routing
    {Param}  = id
    {items} = 1,2,3

    https://domain/{source}/User/Collection/List/{Param}/{items}
    https://domain/{source}/User/Collection/Range/{Param}/{items}
    https://domain/{source}/User/Object/Update/{Param}/{items}

    Pattern:
    https://domain/{source}/{model}/param/get/{param}/{name}/

    Example:
    https://domain/source/{source}/model/{model}/param/{param}/get/id/10/

#### Get Login

    GET https://domain/{source}/{model}/{param}/{value} /param/ login /get/ where / 
    GET https://domain/   db   / user  /   id / 10 /param/ login /get/ where / 
    GET https://domain/source/ db /model/ user /param/ login /get/ where / id / 10 /

#### Set Password
PUT https://domain/source/ db /model/ user /param/ password /set/ id / 10
{
    "param":
}

## SQL Generator
Creating from Tree of model-name-type
The SQL Statements for:
+ Collection
+ Object
+ Param

## SQL Inspector


## Functionality
+ Create metada from SQL schema
+ Create REST API based on SWAGGER From Metadata
+ Generate sdk for SWAGGER API


# TODO

## 1 prototyp
zamiast pliku - zmienne w array dla modelu i konfiguracji
petla parsowania
wygenerowane 9 zapytan

## 2 prototyp
plik konfiguracyjny
czytanie yaml pliku i zamiana na array
plik z modelami danych i relacjami
czytanie pliku z modelami
petla parsowania
wygenerowane wielu modeli i 9 zapytan

## 3 prototyp
plik konfiguracyjny
czytanie yaml pliku i zamiana na array
plik z modelami danych i relacjami
czytanie pliku z modelami
generowanie 9 zapytan do kazdego modelu
dodatkowe rozpoznawanie

