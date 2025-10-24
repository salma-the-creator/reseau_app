

##  Introduction

Android fournit des permissions réseau permettant aux applications d'accéder à Internet et d’obtenir des informations sur l’état de la connexion. Elles sont indispensables pour les applications qui communiquent avec un serveur, utilisent des API ou chargent du contenu en ligne.

Ce README présente les deux principales permissions réseau, leurs rôles et dans quels cas les utiliser.

---

## Types de permissions réseau

| Permission Android     | Rôle                                                  | Exemple d’usage                  |
| ---------------------- | ----------------------------------------------------- | -------------------------------- |
| `INTERNET`             | Autorise l’accès à Internet                           | Requêtes API, chat, streaming    |
| `ACCESS_NETWORK_STATE` | Vérifie l’état du réseau (Wi-Fi, données, hors-ligne) | Mode offline, tests de connexion |

---

### 📶 `ACCESS_NETWORK_STATE` — Vérification de l’état réseau

* Permet de savoir si l’utilisateur est connecté (Wi-Fi ou données mobiles)
* Permet d’adapter l’interface ou bloquer certaines actions hors-ligne


---

##  Permissions dans `AndroidManifest.xml`

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

---

##  Exemple Kotlin : Vérifier la connexion réseau

```kotlin
fun isNetworkAvailable(context: Context): Boolean {
    val connectivityManager = context.getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
    val network = connectivityManager.activeNetwork ?: return false
    val capabilities = connectivityManager.getNetworkCapabilities(network) ?: return false
    return capabilities.hasTransport(NetworkCapabilities.TRANSPORT_WIFI) ||
           capabilities.hasTransport(NetworkCapabilities.TRANSPORT_CELLULAR)
}

