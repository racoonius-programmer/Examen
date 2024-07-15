import random
import csv
from statistics import geometric_mean

trabajadores = ["Juan Pérez","María García","Carlos López","Ana Martínez","Pedro Rodríguez","Laura Hernández","Miguel Sánchez","Isabel Gómez",
                "Francisco Díaz","Elena Fernández"]
lista_con_sueldos = []
sueldos_menor = []
sueldos_mid = []
sueldos_mayor=[]

def asignar_sueldos():
    for trabajador in range(len(trabajadores)):
        sueldo = random.randint(300000,2500000)
        etiquetar = {
            "Nombre empleado":trabajadores[trabajador],
            "Sueldo":sueldo
        }
        lista_con_sueldos.append(etiquetar)
    print("Sueldos aleatorios asignados.")

def clasificar_sueldos():
    if len(lista_con_sueldos) == 0:
        print("Debe asignar sueldos, presione 1 en el menú principal")
        return
    
    for trabajador in lista_con_sueldos:
        if trabajador["Sueldo"] < 800000:
            menor = {
                "Nombre empleado":trabajador["Nombre empleado"],
                "Sueldo":trabajador["Sueldo"]
                }
            sueldos_menor.append(menor)
    for trabajador in lista_con_sueldos:
        if trabajador["Sueldo"] >= 800000 and trabajador["Sueldo"] <= 2000000:
            mid = {
                "Nombre empleado":trabajador["Nombre empleado"],
                "Sueldo":trabajador["Sueldo"]
                }
            sueldos_mid.append(mid)

    for trabajador in lista_con_sueldos:
        if trabajador["Sueldo"] > 2000000:
            mayor = {
                "Nombre empleado":trabajador["Nombre empleado"],
                "Sueldo":trabajador["Sueldo"]
                }
            sueldos_mayor.append(mayor)

    print(f"\nSueldos menores a $800.000  TOTAL: {len(sueldos_menor)}")
    if len(sueldos_menor) > 0:
        print("\nNombre Empleado\t\tSueldo")
    for trabajador in sueldos_menor:    
        print(f"{trabajador["Nombre empleado"]}\t\t${trabajador["Sueldo"]}")
    print(f"\nSueldos entre $800.000 y $2.000.000  TOTAL: {len(sueldos_mid)}")
    if len(sueldos_mid) > 0:
        print("\nNombre Empleado\t\tSueldo")
    for trabajador in sueldos_mid:    
        print(f"{trabajador["Nombre empleado"]}\t\t${trabajador["Sueldo"]}")
    print(f"\nSueldos superiores a $2.000.000  TOTAL: {len(sueldos_mayor)}")
    if len(sueldos_mayor) > 0:
        print("\nNombre Empleado\t\tSueldo")
    for trabajador in sueldos_mayor:    
        print(f"{trabajador["Nombre empleado"]}\t\t${trabajador["Sueldo"]}")
    
    total_sueldo = 0
    for trabajador in lista_con_sueldos:
        total_sueldo = total_sueldo + trabajador["Sueldo"]
    print(f"TOTAL SUELDOS: \t\t${total_sueldo}")

def ver_estadisticas():
#    print(min(lista_con_sueldos["Sueldo"]))
#    for trabajadores in lista_con_sueldos:
#        print(min(trabajadores["Sueldo"]))
# Puestos como comentario para no romper el programa.

    print("Sueldo más alto: ")
    print("Sueldo más bajo: ")
    print("Promedio de Sueldos: ")
    print("Media geométrica: ")

def reporte_sueldos():
    if len(lista_con_sueldos) == 0:
        print("Debe asignar sueldos, presione 1 en el menú principal")
        return
    
    lista_reporte = []
    for trabajador in lista_con_sueldos:
        reporte = {
            "Nombre":trabajador["Nombre empleado"],
            "Sueldo":trabajador["Sueldo"],
            "Descuento Salud": round(trabajador["Sueldo"] * 0.07),
            "Descuento AFP": round(trabajador["Sueldo"] * 0.12),
            "Sueldo liquido": round(trabajador["Sueldo"] * 0.81)
        }
        lista_reporte.append(reporte)

    with open("Reporte_Sueldos.csv",mode="w",newline="") as archivo:
        writer= csv.writer(archivo)
        writer.writerow(["Nombre empleado\t\tSueldo Base\t\tDescuento Salud\t\tDescuento AFP\t\tSueldo Liquido"])
        for trabajador in lista_reporte:
            writer.writerow([f"{trabajador["Nombre"]}\t\t${trabajador["Sueldo"]}\t\t${trabajador["Descuento Salud"]}\t\t\t\t${trabajador["Descuento AFP"]}\t\t\t\t${trabajador["Sueldo liquido"]}"])
        #La alineacion de lineas varia con cada numero random así que no hay forma de ordenarlo bien con tabulaciones.
    print ("Exportado como 'Reporte_Sueldos.csv'")
def menu_principal():
    while True:
        print("""
    **  Menú  **
1.  Asignar sueldos aleatorios
2.  Clasificar sueldos
3.  Ver estadísticas
4.  Reporte de sueldos
5.  Salir del programa
              """)
        opcion = input("Escoga una opción: ")
        if opcion == "1":
            asignar_sueldos()
        elif opcion == "2":
            clasificar_sueldos()
        elif opcion == "3":
            ver_estadisticas()
        elif opcion == "4":
            reporte_sueldos()
        elif opcion == "5":
            print("""
Finalizando programa...
Desarrollado por Franco Reyes
RUT 21.486.305-7
                  """)
            break
        else:
            print("Comando no válido, vuelva a ingresar.")

if __name__ == "__main__":
    menu_principal()