Shifoumi
===============

L'application Shifoumi respecte le contrat suivant :


```

GET     /games                                  Application.getAllGames
POST    /games                                  Application.notifyNewGame
GET     /games/{id}                             Application.getGame
POST    /games/{id}                             Application.finishGame

GET     /ui/games                               Application.getAllGamesUI
GET     /ui/games/{id}                          Application.getGameUI


```

Le squelette du controleur principal est le suivant :

```java

package controllers;

import com.google.gson.Gson;
import play.mvc.*;

import java.util.*;

import models.*;

public class Application extends Controller {

    /**
     * Appelé par le bot
     * Renvoi la liste des jeux enregistrés dans la base en JSON
     */
    public static void getAllGames() {
        ...
    }

    /**
     * Appelé par le bot
     * Créé un nouveau jeu dans la base. Ce jeu ne contient pas encore les rounds joués
     * il contient simplement l'id du jeu et les mains à jouer sous la forme
     * ROCK:PAPER:ROCK:PAPER:ROCK
     * Le nombre de mains == rounds
     * renvoi un ok()
     */
    public static void notifyNewGame(String id, int rounds) {
        ...
    }

    /**
     * Appelé par le bot
     * Récupère le jeu avec l'ID spécifié en JSON
     */
    public static void getGame(String id) {
        ...
    }

    /**
     * Appelé par le bot
     * Le bot envoit le jeu complet (avec les rounds) dans le body de la requete
     * Il faut ici le merger avec celui correspondant en base pour le finaliser
     * Renvoi un ok();
     */
    public static void finishGame(String id) {
        Game gameFromBot = new Gson().fromJson(request.params.get("body"), Game.class);
        ...
    }

    /**
     * Appelé depuis votre navigateur
     * Renvoi une vue de tous les jeux que vous avez joué ainsi que les stats
     */
    public static void getAllGamesUI() {
        ...
    }

    /**
     * Appelé depuis votre navigateur
     * Renvoi une vue d'un jeu en particulier
     */
     public static void getGameUI(String id) {
        ...
    }
}

```

Les jeux enregistrés en base se baseront sur le squelette suivant :

```java

package models;

import play.db.jpa.GenericModel;

import javax.persistence.CascadeType;
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.OneToMany;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@Entity
public class Game extends GenericModel {

    // Voici les seules valeures possibles pour les mains
    public static String ROCK = "ROCK";
    public static String PAPER = "PAPER";
    public static String SCISSORS = "SCISSORS";

    @Id
    public String id;

    public String getId() {
        return id;
    }

    @Override
    public Object _key() {
        return getId();
    }

    // les mains jouées
    // le jeu a-t-il été gagné
    // liste des rounds (one to many)

    ...
}


```

Un Round est formé de la façon suivante :

```java

package models;

import play.db.jpa.Model;

import javax.persistence.Entity;

@Entity
public class Round extends Model {

    public String yourIp;
    public String opponentIp;
    public String yourHand;
    public String opponentHand;
    public Boolean win;

}

```

Voici un exemple de jeu :

```json
{
    "id":"fa668bb2-b9f8-4ca9-87df-07bd2762f6e8",
    "hands":"SCISSORS:SCISSORS:SCISSORS:PAPER:ROCK",
    "rounds":[
        {
            "yourIp":"127.0.0.1",
            "opponentIp":"AI Player",
            "yourHand":"SCISSORS",
            "opponentHand":"PAPER",
            "win":true
        },{
            "yourIp":"127.0.0.1",
            "opponentIp":"AI Player",
            "yourHand":"SCISSORS",
            "opponentHand":"SCISSORS",
            "win":false
        },{
            "yourIp":"127.0.0.1",
            "opponentIp":"AI Player",
            "yourHand":"SCISSORS",
            "opponentHand":"PAPER",
            "win":true
        },{
            "yourIp":"127.0.0.1",
            "opponentIp":"AI Player",
            "yourHand":"PAPER",
            "opponentHand":"PAPER",
            "win":false
        },{
            "yourIp":"127.0.0.1",
            "opponentIp":"AI Player",
            "yourHand":"ROCK",
            "opponentHand":"SCISSORS",
            "win":true
        }
    ],
    "win":true
}

```