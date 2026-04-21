# -Asservissement_Numerique_RAFANOMEZANTSOA_SitrakiniavoSedratiana_Projet11
RAFANOMEZANTSOA Sitrakiniavo Sedratiana
 README.md
 Asservissement Numérique - Projet 11

## Description
Ce projet porte sur la réalisation d’un système d’asservissement en position
implémenté en Python.

## Objectif
L’objectif est de concevoir un système de commande permettant de contrôler
la vitesse d'un moteur à courant continu.

## Outils utilisés
- Python(control library)

## Exécution
1. Installer Python
2. Installer les bibliothèques nécessaires
3. Lancer le fichier principal :
   pid numérique pour moteur dc.py
4. taper ce code
import numpy as np
import matplotlib.pyplot as plt

# Paramètres moteur DC
J = 0.01
b = 0.1
K = 0.01
R = 1
L = 0.5

# Simulation
Ts = 0.01
N = 500
t = np.arange(0, N*Ts, Ts)

# PID
Kp = 100
Ki = 200
Kd = 0.5

ref = np.ones(N)
y = np.zeros(N)
u = np.zeros(N)
e = np.zeros(N)

# Etats du moteur
omega = 0
i = 0

for k in range(2, N):
    # erreur
    e[k] = ref[k] - omega

    # PID discret
    u[k] = u[k-1] \
           + Kp*(e[k] - e[k-1]) \
           + Ki*Ts*e[k] \
           + Kd/Ts*(e[k] - 2*e[k-1] + e[k-2])

    #u[k] = max(min(u[k], 24), -24)

    # Modèle moteur (équations différentielles discrétisées)
    di = (u[k] - R*i - K*omega) / L
    domega = (K*i - b*omega) / J

    i += di * Ts
    omega += domega * Ts

    y[k] = omega

# Graphes
plt.figure()
plt.plot(t, y, label="Vitesse")
plt.plot(t, ref, '--', label="Consigne")
plt.legend()
plt.grid()

plt.figure()
plt.plot(t, u, label="Commande")
plt.legend()
plt.grid()

plt.show()

5. run python file

## Résultats
Les résultats obtenus montrent la réponse du système avec analyse des performances.

## Auteur
RAFANOMEZANTSOA Sitrakinavo Sedratiana
