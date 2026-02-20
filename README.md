# PythonProject1
///LISTA CIRCULAR RUDY MEJIA 
class Nodo:
    def __init__(self, consumo):
        self.consumo = consumo  # consumo eléctrico de la planta
        self.siguiente = None


class ListaCircular:
    def __init__(self):
        self.cabeza = None

    def insertar(self, consumo):
        nuevo = Nodo(consumo)
        if self.cabeza is None:
            self.cabeza = nuevo
            nuevo.siguiente = self.cabeza
        else:
            temp = self.cabeza
            while temp.siguiente != self.cabeza:
                temp = temp.siguiente
            temp.siguiente = nuevo
            nuevo.siguiente = self.cabeza
        print(f"Consumo {consumo} agregado correctamente.")

    def recorrer(self):
        if self.cabeza is None:
            print("La lista está vacía.")
            return
        temp = self.cabeza
        print("Consumos registrados:")
        while True:
            print(f"- {temp.consumo} kWh")
            temp = temp.siguiente
            if temp == self.cabeza:
                break

    def buscar(self, consumo):
        if self.cabeza is None:
            print("La lista está vacía.")
            return
        temp = self.cabeza
        while True:
            if temp.consumo == consumo:
                print(f"Consumo {consumo} encontrado.")
                return
            temp = temp.siguiente
            if temp == self.cabeza:
                break
        print(f"Consumo {consumo} no encontrado.")

    def eliminar(self, consumo):
        if self.cabeza is None:
            print("La lista está vacía.")
            return

        actual = self.cabeza
        previo = None

        while True:
            if actual.consumo == consumo:
                if previo is None:  # eliminar cabeza
                    if actual.siguiente == self.cabeza:  # solo un nodo
                        self.cabeza = None
                    else:
                        # encontrar último nodo
                        temp = self.cabeza
                        while temp.siguiente != self.cabeza:
                            temp = temp.siguiente
                        temp.siguiente = actual.siguiente
                        self.cabeza = actual.siguiente
                else:
                    previo.siguiente = actual.siguiente
                print(f"Consumo {consumo} eliminado.")
                return
            previo = actual
            actual = actual.siguiente
            if actual == self.cabeza:
                break
        print(f"Consumo {consumo} no encontrado.")


def menu():
    lista = ListaCircular()
    while True:
        print("\n--- Menú Principal ---")
        print("1. Agregar consumo")
        print("2. Buscar consumo")
        print("3. Eliminar consumo")
        print("4. Mostrar consumos")
        print("5. Salir")

        opcion = input("Seleccione una opción: ")

        if opcion == "1":
            consumo = input("Ingrese el consumo eléctrico (kWh): ")
            lista.insertar(consumo)
        elif opcion == "2":
            consumo = input("Ingrese el consumo a buscar: ")
            lista.buscar(consumo)
        elif opcion == "3":
            consumo = input("Ingrese el consumo a eliminar: ")
            lista.eliminar(consumo)
        elif opcion == "4":
            lista.recorrer()
        elif opcion == "5":
            print("Saliendo del programa...")
            break
        else:
            print("Opción inválida, intente de nuevo.")


if __name__ == "__main__":
    menu()

