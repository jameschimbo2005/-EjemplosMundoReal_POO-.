from cliente import Cliente
from habitacion import Habitacion

class Hotel:
    def __init__(self, nombre):
        self.nombre = nombre
        self.habitaciones = []
        self.reservas = {}

    def agregar_habitacion(self, habitacion):
        self.habitaciones.append(habitacion)

    def mostrar_habitaciones(self):
        for hab in self.habitaciones:
            print(hab.mostrar_info())

    def reservar_habitacion(self, cliente, numero_habitacion):
        for hab in self.habitaciones:
            if hab.numero == numero_habitacion and hab.reservar():
                self.reservas[cliente.cedula] = (cliente, hab)
                print(f"Reserva exitosa para {cliente.nombre}")
                return
        print("Habitación no disponible")

    def cancelar_reserva(self, cedula):
        if cedula in self.reservas:
            cliente, hab = self.reservas.pop(cedula)
            hab.liberar()
            print(f"Reserva cancelada para {cliente.nombre}")
        else:
            print("No se encontró ninguna reserva para esa cédula")

