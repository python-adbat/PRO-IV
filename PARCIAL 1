import sqlite3

conn  =  sqlite3.connect('sistema_inventario.db')

conn.execute('''CREATE TABLE IF NOT EXISTS ROPA_INV
                (ID INTEGER PRIMARY KEY AUTOINCREMENT,
                ARTICULO TEXT NOT NULL,
                MARCA TEXT NOT NULL,
                SECCION TEXT NOT NULL,
                DESCRIPCION TEXT NOT NULL,
                PRECIO REAL NOT NULL,
                CANTIDAD INTEGER NOT NULL);''')
# print('tabla creada')

# conn.execute('DROP TABLE ROPA_INV')
# conn.commit()
# print('tabla eliminada')

def registro(conn):
    finbucle = False
    while not finbucle:
        try:
            print('\n<|REGISTRO|>')
            print('\nIngrese los siguientes datos de la prenda')
            articulo = input('Tipo: ').lower()
            marca = input('Marca: ').lower()
            seccion = input('Seccion: ').lower()
            descripcion = input('Descripcion: ').lower()
            revisar = conn.execute('SELECT * FROM ROPA_INV WHERE ARTICULO = ? AND MARCA = ? AND SECCION = ? AND DESCRIPCION = ?', (articulo, marca,  seccion, descripcion)).fetchall()
            if revisar:
                print('\nESTE ARTICULO HA SIDO REGISTRADO ANTERIORMENTE\n')
                while True:
                    print('a. INTENTAR AGREGAR OTRO ARTICULO')
                    print('b. SALIR AL MENU PRINCIPAL')
                    opc2 = input('Ingrese una opción: ').lower()
                    if opc2 == 'a':
                        break
                    elif opc2 == 'b':
                        finbucle = True
                        break
                    else:
                        print('\nOPCION NO VALIDA. INTENTE DE NUEVO\n')
            else:
                precio = input('Precio: ')
                cantidad = input('Cantidad en stack: ')
                conn.execute('INSERT INTO ROPA_INV (articulo, marca, seccion, descripcion, precio, cantidad) VALUES (?, ?, ?, ?, ?, ?)', (articulo, marca, seccion, descripcion, precio, cantidad))
                conn.commit()
                print('\nNUEVO ARTICULO AGREGADO CORRECTAMENTE\n')
                break
        except Exception as e:
            print(e)

def buscar(conn):
    finbucle = False
    while not finbucle:
        try:
            print('\n<|BUSCAR ARTICULO|>')
            articulo = input('\nTipo: ').lower()
            revisar = conn.execute('SELECT * FROM ROPA_INV WHERE ARTICULO = ?', (articulo,)).fetchall()
            if revisar:
                print('\nARTICULOS ENCONTRADOS:')
                for fila in revisar:
                    print(f'\tID: {fila[0]}; TIPO: {fila[1]}; MARCA: {fila[2]}; SECCION: {fila[3]}; DESCRIPCION: {fila[4]}; PRECIO: {fila[5]}; CANTIDAD: {fila[6]}')
                break
            else:
                print('\nNO HAY ARTICULOS DE ESE TIPO')
                while True:
                    print('\na. INTENTAR BUSCAR OTRO TIPO DE ARTICULO')
                    print('b. SALIR AL MENU PRINCIPAL')
                    opc2 = input('Ingrese una opción: ').lower()
                    if opc2 == 'a':
                        break
                    elif opc2 == 'b':
                        finbucle = True
                        break
                    else:
                        print('\nOPCION NO VALIDA. INTENTE DE NUEVO\n')
        except Exception as e:
            print(e)

def editar(conn):
    finbucle = False
    while not finbucle:
        try:
            print('\n<|EDITAR ARTICULO|>')
            id = input('\nID: ')
            revisar = conn.execute('SELECT * FROM ROPA_INV WHERE ID = ?', (id,)).fetchone()
            if revisar is None:
                print('\nESTE ARTICULO NO EXISTE')
                while True:
                    print('\na. INTENTAR EDITAR OTRO ARTICULO')
                    print('b. SALIR AL MENU PRINCIPAL')
                    opc2 = input('Ingrese una opción: ').lower()
                    if opc2 == 'a':
                        break
                    elif opc2 == 'b':
                        finbucle = True
                        break
                    else:
                        print('\nOPCION NO VALIDA. INTENTE DE NUEVO\n')
            else:
                print('\nIngrese los nuevos datos del articulo')
                newtipo = input('Tipo: ').lower()
                newmarca = input('Marca: ').lower()
                newseccion = input('Seccion: ').lower()
                newdescrip = input('Descripcion: ').lower()
                newprecio = input('Precio: ').lower()
                newcant = input('Cantidad: ').lower()
                conn.execute('UPDATE ROPA_INV SET ARTICULO = ?, MARCA = ?, SECCION = ?, DESCRIPCION = ?, PRECIO = ?, CANTIDAD = ? WHERE ID = ?', (newtipo, newmarca, newseccion, newdescrip, newprecio, newcant, id))
                conn.commit()
                print('\nPALABRA EDITADA CORRECTAMENTE')
                break
        except Exception as e:
            print(e)

def eliminar(conn):
    finbucle = False
    while not finbucle:
        try:
            print('\n<|ELIMINAR ARTICULO|>')
            id = input('\nID: ')
            revisar = conn.execute('SELECT * FROM ROPA_INV WHERE ID = ?', (id,)).fetchone()
            if revisar is None:
                print('\nESTE ARTICULO NO EXISTE')
                while True:
                    print('\na. INTENTAR ELIMINAR OTRO ARTICULO')
                    print('b. SALIR AL MENU PRINCIPAL')
                    opc2 = input('Ingrese una opción: ').lower()
                    if opc2 == 'a':
                        break
                    elif opc2 == 'b':
                        finbucle = True
                        break
                    else:
                        print('\nOPCION NO VALIDA. INTENTE DE NUEVO\n')
            else:
                conn.execute('DELETE FROM ROPA_INV WHERE ID = ?', (id,))
                conn.commit()
                print('\nARTICULO ELIMINADO CORRECTAMENTE')
                break
        except Exception as e:
            print(e)

while True:
    print("\n\n<| SISTEMA DE INVENTARIO |>")
    print("1. Registrar articulo.")
    print("2. Buscar articulo.")
    print("3. Editar articulo.")
    print("4. Eliminar articulo.")
    print("5. Salir.")
    try:
        opcion = int(input("Opcion: "))
    except:
        print("ERR::Opcion invalida.")
        opcion = 999

    if opcion == 1:
        registro(conn)
    if opcion == 2:
        buscar(conn)
    if opcion == 3:
        editar(conn)
    if opcion == 4:
        eliminar(conn)
    if opcion == 5:
        print('\nSALIENDO DEL INVENTARIO')
        break
        conn.close()
