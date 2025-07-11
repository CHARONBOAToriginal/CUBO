# Funzione Cubo Integrato

Questo progetto rappresenta una simulazione computazionale di una struttura tridimensionale composta da cubetti evolutivi, ognuno definito come funzione dello spazio e del tempo integrato.

## 📌 Descrizione

Ogni cella Cᵢⱼₖ(t) evolve nel tempo in base a:
- Posizione spaziale (x, y, z)
- Tempo vissuto integrato τ(t)
- Stato dei cubetti adiacenti

## 🔧 Funzioni principali

```python
def phi(t):
    return t ** 0.5  # o altra funzione temporale

def evoluzione_locale(cell, vicini, t):
    media_stati = sum(v["state"] for v in vicini) / len(vicini)
    nuova_tau = cell["tau"] + phi(t) * dt
    nuovo_stato = f(cell["state"], media_stati, nuova_tau)
    return nuovo_stato, nuova_tau
```

## 🔁 Ciclo di evoluzione

```python
while t < T_max:
    nuova_C = deepcopy(C)

    for x in range(N_x):
        for y in range(N_y):
            for z in range(N_z):
                cell = C[x][y][z]
                vicini = get_vicini(C, x, y, z)
                nuovo_stato, nuova_tau = evoluzione_locale(cell, vicini, t)
                nuova_C[x][y][z]["state"] = nuovo_stato
                nuova_C[x][y][z]["tau"] = nuova_tau

    C = nuova_C
    t += dt
```

## 🧩 Funzione di vicinato

```python
def get_vicini(C, x, y, z):
    vicini = []
    for dx in [-1, 0, 1]:
        for dy in [-1, 0, 1]:
            for dz in [-1, 0, 1]:
                if dx == dy == dz == 0:
                    continue
                xi, yi, zi = x + dx, y + dy, z + dz
                if 0 <= xi < N_x and 0 <= yi < N_y and 0 <= zi < N_z:
                    vicini.append(C[xi][yi][zi])
    return vicini
```

## 🧠 Significato

Il modello simula l'evoluzione collettiva e individuale di ogni cubetto nel tempo, con comportamento emergente non lineare. La trasformazione temporale integrata τ(t) consente una visione dinamica della rete, utile in applicazioni teoriche di tipo fisico, cognitivo e informativo.
