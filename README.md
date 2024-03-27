# triqui2

def imprimirtablero(tablero):
    print("  0 1 2")
    for i in range(3):
        row = " ".join (tablero[i] )
        print(f"{i} {row}")

def verificarganador (tablero, jugador ):
    
    for i in range (3):
        if all (cell == jugador for cell in tablero[i]):
            return True
    
    for i in range (3):
        if all (tablero[j][i] == jugador for j in range(3)):
            return True

    if all(tablero[i][i] == jugador for i in range(3)) or all(tablero[i][2-i] == jugador for i in range(3)):
        return True
    return False

def triqui():
    jugadores = []
    for i in range(2):
        nombre = input(f"Ingrese el nombre del jugador {i+1}: ")
        jugadores.append(nombre)

    simbolos = ['X', 'O']
    turno = 0
    tablero = [[' ']*3 for _ in range(3)]

    while True:
        imprimirtablero(tablero)
        print(f"Turno de {jugadores[turno]} ({simbolos[turno]})")

        fila = int(input("Ingrese el número de fila (0, 1, 2): "))
        columna = int(input("Ingrese el número de columna (0, 1, 2): "))

        if fila not in range(3) or columna not in range(3):
            print("La casilla no existe. Porfavor Intente de nuevo.")
            continue

        if tablero[fila][columna] != ' ':
            print("La casilla ya está ocupada. Porfavor Intente de nuevo.")
            continue

        tablero[fila][columna] = simbolos[turno]

        if verificarganador(tablero, simbolos[turno]):
            imprimirtablero(tablero)
            print(f"¡{jugadores[turno]} has ganado!")
            break

        if all(all(cell != ' ' for cell in row) for row in tablero):
            imprimirtablero(tablero)
            print("¡Es un Empate!")
            break

        turno = (turno + 1) % 2

if __name__ == "__main__":
    while True:
        triqui()
        jugarnuevamente = input("¿Quieren jugar nuevamente? (si/no): ")
        if jugarnuevamente.lower() in ['s', 'si']:
            continue  
        else:
            break  