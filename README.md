# FASE_5_FREDDYRIVERA_PYTHON
Código para dar solución al problema 3 de la fase 5 del programa FUNDAMENTOS DE LA PROGRAMACION.


Problema 3: 

Se requiere una herramienta para auditar el inventario y
decidir qué artículos necesitan ser reabastecidos. 

La información se encuentra en una matriz: [Código artículo, nombre, stock actual, stock mínimo requerido].

Requisitos de Desarrollo

-	 Matriz: Crear una matriz con al menos 5 artículos.

-	Módulos: Se requiere un módulo (función) para determinar la cantidad exacta por pedir para un artículo.

-	Lógica de Negocio:

✓ Si el Stock Actual es menor al Stock Mínimo, la cantidad a pedir es la diferencia (Mínimo Requerido - Stock Actual).

✓ Si el Stock Actual es suficiente (mayor o igual al Mínimo), la cantidad a pedir es cero.

-	 Salida: Imprimir una lista de pedidos que muestre el nombre del artículo y la cantidad exacta que debe ser solicitada.


En el código utilizo diferentes elementos de programación para construir un sistema básico de gestión de inventario. Primero, se emplea una matriz o lista bidimensional llamada INVENTARIO, donde se almacenan los datos de cada producto como código, nombre, stock actual y stock mínimo. También se utilizan funciones o módulos como mostrar_inventario(), agregar_producto(), editar_producto() y eliminar_producto(), las cuales permiten organizar el programa y reutilizar procesos específicos.

Además, el programa hace uso de estructuras condicionales (if, elif, else) para tomar decisiones según la opción seleccionada por el usuario o para verificar si un producto necesita ser reabastecido. Las estructuras repetitivas (for y while) permiten recorrer los productos del inventario y mantener el menú activo hasta que el usuario decida salir. Finalmente, se emplean variables, entradas de datos con input(), manejo de errores con try-except y una función llamada calcular_pedido() que aplica la lógica de negocio para determinar cuántas unidades deben solicitarse cuando el stock es menor al mínimo requerido.


    INVENTARIO = [
        ["A101", "Teclado", 8, 10],
        ["A102", "Mouse", 25, 15],
        ["A103", "Monitor", 3, 5],
        ["A104", "Silla", 0, 4],
        ["A105", "Audifonos", 12, 10]
    ]
    
    def mostrar_inventario():
        print("\n" + "="*60)
        print(f"{'ID':<5} {'Producto':<20} {'Stock Actual':<15} {'Stock Mínimo':<10}")
        print("="*60)
        for producto in INVENTARIO:
            print(f"{producto[0]:<5} {producto[1]:<20} {producto[2]:<15} {producto[3]:<10}")
        print("="*60 + "\n")
    
    def agregar_producto(codigo, nombre, stock_actual, stock_minimo):
        INVENTARIO.append([codigo, nombre, stock_actual, stock_minimo])
        print(f"✓ Producto '{nombre}' agregado correctamente\n")
    
    def editar_producto(codigo, nombre=None, stock_actual=None, stock_minimo=None):
        for producto in INVENTARIO:
            if str(producto[0]).upper() == str(codigo).upper():
                cambios = False
                if nombre and nombre.strip():  # Si nombre tiene contenido
                    producto[1] = nombre
                    cambios = True
                if stock_actual is not None:
                    producto[2] = stock_actual
                    cambios = True
                if stock_minimo is not None:
                    producto[3] = stock_minimo
                    cambios = True
                if cambios:
                    print(f"✓ Producto ID {codigo} actualizado correctamente\n")
                    print(f"  Datos actuales: {producto}\n")
                else:
                    print(f"ℹ No se realizaron cambios\n")
                return
        print(f"✗ Producto con ID {codigo} no encontrado\n")
        print(f"  Códigos disponibles: {[p[0] for p in INVENTARIO]}\n")
    
    def eliminar_producto(codigo):
        for i, producto in enumerate(INVENTARIO):
            if producto[0] == codigo:
                INVENTARIO.pop(i)
                print(f"✓ Producto eliminado correctamente\n")
                return
        print(f"✗ Producto con ID {codigo} no encontrado\n")
    
    def calcular_pedido(stock_actual, stock_minimo):
        if stock_actual < stock_minimo:
            return stock_minimo - stock_actual
        else:
            return 0
    
    def INICIO():
        while True:
            print("\n==============================")
            print(" Menú: Inventario de Productos ")
            print("================================")
            print("1. Mostrar Inventario.")
            print("2. Agregar Producto.")
            print("3. Editar Producto.")
            print("4. Eliminar Producto.")
            print("5. Salir.")
            try:
                opcion = int(input("¿Cuál es su opción? "))
            except ValueError:
                print("Opción no válida.")
                continue
            if opcion == 1:
                mostrar_inventario()
        
        elif opcion == 2:
            try:
                codigo = input("Ingrese el código del producto: ")
                nombre = input("Ingrese el nombre del producto: ")
                stock_actual = int(input("Ingrese el stock actual: "))
                stock_minimo = int(input("Ingrese el stock mínimo: "))
                agregar_producto(codigo, nombre, stock_actual, stock_minimo)
            except ValueError:
                print("Entrada no válida. Por favor, ingrese los datos correctamente.\n")
        elif opcion == 3:
            try:
                print("\nProductos disponibles:")
                for p in INVENTARIO:
                    print(f"  {p[0]} - {p[1]}")
                codigo = input("\nIngrese el código del producto a editar: ")
                print("Deje en blanco los campos que no desea modificar.")
                nombre = input("Nuevo nombre del producto: ")
                stock_actual_input = input("Nuevo stock actual: ")
                stock_minimo_input = input("Nuevo stock mínimo: ")
                stock_actual = int(stock_actual_input) if stock_actual_input else None
                stock_minimo = int(stock_minimo_input) if stock_minimo_input else None
                editar_producto(codigo, nombre if nombre else None, stock_actual, stock_minimo)
            except ValueError:
                print("Entrada no válida. Por favor, ingrese los datos correctamente.\n")
        elif opcion == 4:
            try:
                codigo = input("Ingrese el código del producto a eliminar: ")
                eliminar_producto(codigo)
            except ValueError:
                print("Entrada no válida. Por favor, ingrese un código válido.\n")
        elif opcion == 5:
            print("\n" + "="*60)
            print("\nLISTA DE PRODUCTOS POR PEDIR:")
            print("="*60 + "\n")
            for p in INVENTARIO:
                print(f"  {p[0]} - {p[1]} : {calcular_pedido(p[2], p[3])} unidades a pedir")
            print("\n" + "="*60)
            print("¡Gracias por usar el sistema de inventario!")
            print("="*60 + "\n")
            break
        
        else:
            print("Opción no válida. Por favor, seleccione una opción del menú.\n")


    if __name__ == "__main__":
        INICIO()
