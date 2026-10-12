
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Don Juan | Sistema de Gestión</title>

    <style>
        :root {
            --negro: #171717;
            --negro-claro: #242424;
            --dorado: #c9a44c;
            --dorado-claro: #f0d58a;
            --fondo: #f4f4f2;
            --blanco: #ffffff;
            --texto: #292929;
            --gris: #777777;
            --borde: #e2e2df;
            --verde: #237b4b;
            --rojo: #b83232;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: Arial, Helvetica, sans-serif;
            background: var(--fondo);
            color: var(--texto);
            line-height: 1.5;
        }

        button, input, select, textarea {
            font: inherit;
        }

        button {
            cursor: pointer;
        }

        .encabezado {
            background: var(--negro);
            color: var(--blanco);
            padding: 18px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 15px;
            border-bottom: 3px solid var(--dorado);
        }

        .marca h1 {
            font-size: 21px;
            letter-spacing: 1px;
        }

        .marca span {
            color: var(--dorado-claro);
        }

        .marca p {
            font-size: 12px;
            color: #d0d0d0;
        }

        .usuario {
            font-size: 13px;
            text-align: right;
        }

        .usuario strong {
            display: block;
            color: var(--dorado-claro);
        }

        .contenedor {
            display: grid;
            grid-template-columns: 225px minmax(0, 1fr);
            min-height: calc(100vh - 76px);
        }

        .menu {
            background: var(--negro-claro);
            padding: 22px 13px;
        }

        .menu h2 {
            color: #bdbdbd;
            font-size: 11px;
            text-transform: uppercase;
            letter-spacing: 1.4px;
            padding: 0 12px 12px;
        }

        .enlace-menu {
            display: block;
            width: 100%;
            text-align: left;
            border: none;
            background: transparent;
            color: #eeeeee;
            padding: 12px;
            margin-bottom: 5px;
            border-radius: 6px;
            transition: background 0.2s;
        }

        .enlace-menu:hover,
        .enlace-menu.activo {
            background: var(--dorado);
            color: var(--negro);
            font-weight: bold;
        }

        main {
            padding: 28px;
            min-width: 0;
        }

        .pagina {
            display: none;
        }

        .pagina.activa {
            display: block;
        }

        .titulo-pagina {
            margin-bottom: 22px;
        }

        .titulo-pagina h2 {
            font-size: 26px;
            margin-bottom: 5px;
        }

        .titulo-pagina p {
            color: var(--gris);
            font-size: 14px;
        }

        .tarjetas {
            display: grid;
            grid-template-columns: repeat(3, minmax(0, 1fr));
            gap: 16px;
            margin-bottom: 25px;
        }

        .tarjeta {
            background: var(--blanco);
            border: 1px solid var(--borde);
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.03);
        }

        .tarjeta .etiqueta {
            color: var(--gris);
            font-size: 13px;
        }

        .tarjeta .numero {
            display: block;
            font-size: 27px;
            font-weight: bold;
            margin-top: 8px;
        }

        .tarjeta .detalle {
            display: block;
            color: var(--gris);
            font-size: 12px;
            margin-top: 4px;
        }

        .panel {
            background: var(--blanco);
            padding: 22px;
            border: 1px solid var(--borde);
            border-radius: 10px;
            margin-bottom: 22px;
        }

        .panel h3 {
            margin-bottom: 16px;
            font-size: 18px;
        }

        .barra-acciones {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 12px;
            flex-wrap: wrap;
            margin-bottom: 18px;
        }

        .campo-busqueda {
            flex: 1;
            min-width: 180px;
        }

        input, select, textarea {
            width: 100%;
            padding: 11px 12px;
            border: 1px solid #cccccc;
            border-radius: 6px;
            background: white;
            color: var(--texto);
        }

        input:focus, select:focus, textarea:focus {
            outline: 2px solid var(--dorado);
            outline-offset: 1px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            font-size: 13px;
            font-weight: bold;
        }

        .formulario {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            gap: 16px;
        }

        .campo.completo {
            grid-column: 1 / -1;
        }

        .boton {
            padding: 11px 16px;
            border: none;
            border-radius: 6px;
            font-weight: bold;
        }

        .boton-principal {
            background: var(--dorado);
            color: var(--negro);
        }

        .boton-principal:hover {
            background: var(--dorado-claro);
        }

        .boton-secundario {
            background: #e9e9e6;
            color: var(--texto);
        }

        .tabla-contenedor {
            width: 100%;
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 520px;
        }

        th, td {
            text-align: left;
            padding: 13px 10px;
            border-bottom: 1px solid var(--borde);
            font-size: 13px;
        }

        th {
            background: #f5f2e9;
            color: #353127;
        }

        .estado {
            display: inline-block;
            padding: 4px 9px;
            border-radius: 20px;
            background: #eeeeee;
            font-size: 11px;
            font-weight: bold;
        }

        .estado-confirmada,
        .estado-atendida {
            color: var(--verde);
            background: #e2f3e8;
        }

        .estado-pendiente {
            color: #855c00;
            background: #fff1c9;
        }

        .estado-cancelada {
            color: var(--rojo);
            background: #fbe5e5;
        }

        .nota {
            color: var(--gris);
            font-size: 12px;
            margin-top: 12px;
        }

        .pie {
            text-align: center;
            color: var(--gris);
            font-size: 12px;
            padding: 20px;
        }

        #mensaje {
            display: none;
            margin-bottom: 18px;
            padding: 12px;
            border-radius: 6px;
            background: #e2f3e8;
            color: var(--verde);
            font-size: 14px;
        }

        .servicios {
            display: grid;
            grid-template-columns: repeat(3, minmax(0, 1fr));
            gap: 15px;
        }

        .servicio {
            border: 1px solid var(--borde);
            border-radius: 8px;
            padding: 18px;
            background: white;
        }

        .servicio h4 {
            margin-bottom: 8px;
        }

        .servicio .precio {
            color: #8d6b18;
            font-size: 22px;
            font-weight: bold;
        }

        .servicio p {
            color: var(--gris);
            font-size: 13px;
            margin-top: 5px;
        }

        @media (max-width: 900px) {
            .contenedor {
                grid-template-columns: 180px minmax(0, 1fr);
            }

            main {
                padding: 20px;
            }

            .tarjetas, .servicios {
                grid-template-columns: repeat(2, minmax(0, 1fr));
            }
        }

        @media (max-width: 650px) {
            .encabezado {
                padding: 15px;
                align-items: flex-start;
            }

            .marca h1 {
                font-size: 17px;
            }

            .usuario {
                font-size: 11px;
            }

            .contenedor {
                display: block;
            }

            .menu {
                padding: 12px;
            }

            .menu h2 {
                padding-bottom: 8px;
            }

            .enlace-menu {
                display: inline-block;
                width: auto;
                padding: 9px 11px;
                font-size: 12px;
            }

            main {
                padding: 16px;
            }

            .titulo-pagina h2 {
                font-size: 22px;
            }

            .tarjetas, .servicios, .formulario {
                grid-template-columns: 1fr;
            }

            .campo.completo {
                grid-column: auto;
            }

            .panel {
                padding: 16px;
            }
        }
    </style>
</head>

<body>
    <header class="encabezado">
        <div class="marca">
            <h1>DON <span>JUAN</span></h1>
            <p>Sistema de Gestión de Peluquería y Barbería</p>
        </div>

        <div class="usuario">
            Sesión de demostración
            <strong>Administrador</strong>
        </div>
    </header>

    <div class="contenedor">
        <aside class="menu">
            <h2>Menú principal</h2>

            <button class="enlace-menu activo" data-pagina="inicio">
                Inicio
            </button>
            <button class="enlace-menu" data-pagina="citas">
                Citas
            </button>
            <button class="enlace-menu" data-pagina="clientes">
                Clientes
            </button>
            <button class="enlace-menu" data-pagina="servicios">
                Servicios
            </button>
            <button class="enlace-menu" data-pagina="pagos">
                Pagos
            </button>
            <button class="enlace-menu" data-pagina="reportes">
                Reportes
            </button>
            <button class="enlace-menu" data-pagina="usuarios">
                Usuarios
            </button>
        </aside>

        <main>
            <div id="mensaje" role="status" aria-live="polite"></div>

            <section class="pagina activa" id="inicio">
                <div class="titulo-pagina">
                    <h2>Panel principal</h2>
                    <p>Resumen general de la gestión del establecimiento.</p>
                </div>

                <div class="tarjetas">
                    <article class="tarjeta">
                        <span class="etiqueta">Citas registradas</span>
                        <strong class="numero" id="totalCitas">3</strong>
                        <span class="detalle">Datos de demostración</span>
                    </article>

                    <article class="tarjeta">
                        <span class="etiqueta">Clientes de ejemplo</span>
                        <strong class="numero" id="totalClientes">3</strong>
                        <span class="detalle">Registros de esta sesión</span>
                    </article>

                    <article class="tarjeta">
                        <span class="etiqueta">Servicios disponibles</span>
                        <strong class="numero">3</strong>
                        <span class="detalle">Catálogo de referencia</span>
                    </article>
                </div>

                <div class="panel">
                    <h3>Próximas citas de ejemplo</h3>
                    <div class="tabla-contenedor">
                        <table>
                            <thead>
                                <tr>
                                    <th>Hora</th>
                                    <th>Cliente</th>
                                    <th>Servicio</th>
                                    <th>Estado</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>09:00 a. m.</td>
                                    <td>Cliente de ejemplo 1</td>
                                    <td>Corte</td>
                                    <td><span class="estado estado-confirmada">Confirmada</span></td>
                                </tr>
                                <tr>
                                    <td>10:00 a. m.</td>
                                    <td>Cliente de ejemplo 2</td>
                                    <td>Barba</td>
                                    <td><span class="estado estado-pendiente">Pendiente</span></td>
                                </tr>
                                <tr>
                                    <td>11:00 a. m.</td>
                                    <td>Cliente de ejemplo 3</td>
                                    <td>Corte y barba</td>
                                    <td><span class="estado estado-atendida">Atendida</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <p class="nota">
                        La información de esta pantalla es ilustrativa y no corresponde
                        a una base de datos real.
                    </p>
                </div>
            </section>

            <section class="pagina" id="citas">
                <div class="titulo-pagina">
                    <h2>Gestión de citas</h2>
                    <p>Registro y consulta de citas de los clientes.</p>
                </div>

                <div class="panel">
                    <h3>Registrar nueva cita</h3>

                    <form id="formCita" class="formulario">
                        <div class="campo">
                            <label for="clienteCita">Nombre del cliente</label>
                            <input id="clienteCita" required
                                   placeholder="Escribe el nombre">
                        </div>

                        <div class="campo">
                            <label for="servicioCita">Servicio</label>
                            <select id="servicioCita" required>
                                <option value="">Seleccionar servicio</option>
                                <option>Corte</option>
                                <option>Barba</option>
                                <option>Corte y barba</option>
                            </select>
                        </div>

                        <div class="campo">
                            <label for="fechaCita">Fecha</label>
                            <input id="fechaCita" type="date" required>
                        </div>

                        <div class="campo">
                            <label for="horaCita">Hora</label>
                            <input id="horaCita" type="time" required>
                        </div>

                        <div class="campo completo">
                            <button class="boton boton-principal" type="submit">
                                Registrar cita de ejemplo
                            </button>
                        </div>
                    </form>

                    <p class="nota">
                        Este formulario demuestra la interacción visual. No comprueba
                        disponibilidad real ni guarda información permanentemente.
                    </p>
                </div>

                <div class="panel">
                    <h3>Citas de esta sesión</h3>
                    <div class="tabla-contenedor">
                        <table>
                            <thead>
                                <tr>
                                    <th>Fecha</th>
                                    <th>Hora</th>
                                    <th>Cliente</th>
                                    <th>Servicio</th>
                                    <th>Estado</th>
                                </tr>
                            </thead>
                            <tbody id="tablaCitas">
                                <tr>
                                    <td>Ejemplo</td>
                                    <td>09:00</td>
                                    <td>Cliente de ejemplo 1</td>
                                    <td>Corte</td>
                                    <td><span class="estado estado-confirmada">Confirmada</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <section class="pagina" id="clientes">
                <div class="titulo-pagina">
                    <h2>Gestión de clientes</h2>
                    <p>Consulta y registro de clientes de la barbería.</p>
                </div>

                <div class="panel">
                    <h3>Registrar cliente de ejemplo</h3>

                    <form id="formCliente" class="formulario">
                        <div class="campo">
                            <label for="nombreCliente">Nombre completo</label>
                            <input id="nombreCliente" required
                                   placeholder="Nombres y apellidos">
                        </div>

                        <div class="campo">
                            <label for="telefonoCliente">Teléfono</label>
                            <input id="telefonoCliente" type="tel" required
                                   placeholder="Número de contacto">
                        </div>

                        <div class="campo completo">
                            <button class="boton boton-principal" type="submit">
                                Registrar cliente de ejemplo
                            </button>
                        </div>
                    </form>
                </div>

                <div class="panel">
                    <h3>Listado de clientes</h3>

                    <div class="barra-acciones">
                        <div class="campo-busqueda">
                            <label for="buscarCliente">Buscar cliente</label>
                            <input id="buscarCliente" placeholder="Escribe un nombre...">
                        </div>
                    </div>

                    <div class="tabla-contenedor">
                        <table>
                            <thead>
                                <tr>
                                    <th>Nombre</th>
                                    <th>Teléfono</th>
                                </tr>
                            </thead>
                            <tbody id="tablaClientes">
                                <tr>
                                    <td>Cliente de ejemplo 1</td>
                                    <td>0000000000</td>
                                </tr>
                                <tr>
                                    <td>Cliente de ejemplo 2</td>
                                    <td>0000000000</td>
                                </tr>
                                <tr>
                                    <td>Cliente de ejemplo 3</td>
                                    <td>0000000000</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <section class="pagina" id="servicios">
                <div class="titulo-pagina">
                    <h2>Gestión de servicios</h2>
                    <p>Catálogo de servicios de referencia del establecimiento.</p>
                </div>

                <div class="servicios">
                    <article class="servicio">
                        <h4>Corte de cabello</h4>
                        <span class="precio">$25.000</span>
                        <p>Duración de referencia: 45 minutos.</p>
                    </article>

                    <article class="servicio">
                        <h4>Arreglo de barba</h4>
                        <span class="precio">$15.000</span>
                        <p>Duración de referencia: 20 minutos.</p>
                    </article>

                    <article class="servicio">
                        <h4>Corte y barba</h4>
                        <span class="precio">$35.000</span>
                        <p>Duración de referencia: 60 minutos.</p>
                    </article>
                </div>

                <p class="nota">
                    Los precios y las duraciones son valores de referencia y deben
                    confirmarse con el establecimiento antes de una implementación real.
                </p>
            </section>

            <section class="pagina" id="pagos">
                <div class="titulo-pagina">
                    <h2>Gestión de pagos</h2>
                    <p>Formulario visual para registrar pagos de servicios.</p>
                </div>

                <div class="panel">
                    <h3>Registrar pago de ejemplo</h3>

                    <form id="formPago" class="formulario">
                        <div class="campo">
                            <label for="clientePago">Cliente</label>
                            <input id="clientePago" required>
                        </div>

                        <div class="campo">
                            <label for="valorPago">Valor en pesos colombianos</label>
                            <input id="valorPago" type="number" min="1" required>
                        </div>

                        <div class="campo">
                            <label for="fechaPago">Fecha del pago</label>
                            <input id="fechaPago" type="date" required>
                        </div>

                        <div class="campo">
                            <label for="metodoPago">Método de pago</label>
                            <select id="metodoPago" required>
                                <option value="">Seleccionar método</option>
                                <option>Efectivo</option>
                                <option>Transferencia</option>
                                <option>Tarjeta</option>
                            </select>
                        </div>

                        <div class="campo completo">
                            <button class="boton boton-principal" type="submit">
                                Registrar pago de ejemplo
                            </button>
                        </div>
                    </form>
                </div>

                <div class="panel">
                    <h3>Pagos de esta sesión</h3>
                    <div class="tabla-contenedor">
                        <table>
                            <thead>
                                <tr>
                                    <th>Cliente</th>
                                    <th>Valor</th>
                                    <th>Fecha</th>
                                    <th>Método</th>
                                </tr>
                            </thead>
                            <tbody id="tablaPagos">
                                <tr>
                                    <td>Cliente de ejemplo</td>
                                    <td>$25.000</td>
                                    <td>Ejemplo</td>
                                    <td>Efectivo</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <p class="nota">
                        El registro es demostrativo y no confirma una transacción financiera.
                    </p>
                </div>
            </section>

            <section class="pagina" id="reportes">
                <div class="titulo-pagina">
                    <h2>Reportes administrativos</h2>
                    <p>Área de consulta prevista para los informes del negocio.</p>
                </div>

                <div class="tarjetas">
                    <article class="tarjeta">
                        <span class="etiqueta">Citas de ejemplo</span>
                        <strong class="numero" id="reporteCitas">3</strong>
                        <span class="detalle">Registros de demostración</span>
                    </article>

                    <article class="tarjeta">
                        <span class="etiqueta">Servicios del catálogo</span>
                        <strong class="numero">3</strong>
                        <span class="detalle">Servicios de referencia</span>
                    </article>

                    <article class="tarjeta">
                        <span class="etiqueta">Moneda</span>
                        <strong class="numero">COP</strong>
                        <span class="detalle">Pesos colombianos</span>
                    </article>
                </div>

                <div class="panel">
                    <h3>Filtros del reporte</h3>

                    <form id="formReporte" class="formulario">
                        <div class="campo">
                            <label for="fechaInicio">Fecha inicial</label>
                            <input id="fechaInicio" type="date">
                        </div>

                        <div class="campo">
                            <label for="fechaFin">Fecha final</label>
                            <input id="fechaFin" type="date">
                        </div>

                        <div class="campo completo">
                            <button class="boton boton-principal" type="submit">
                                Consultar demostración
                            </button>
                        </div>
                    </form>

                    <p class="nota">
                        La consulta no calcula resultados reales; en una futura versión
                        deberá conectarse a los registros almacenados.
                    </p>
                </div>
            </section>

            <section class="pagina" id="usuarios">
                <div class="titulo-pagina">
                    <h2>Gestión de usuarios</h2>
                    <p>Diseño inicial para organizar las cuentas del personal.</p>
                </div>

                <div class="panel">
                    <h3>Usuarios previstos</h3>

                    <div class="tabla-contenedor">
                        <table>
                            <thead>
                                <tr>
                                    <th>Perfil</th>
                                    <th>Funciones previstas</th>
                                    <th>Estado</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>Administrador</td>
                                    <td>Gestión general del sistema</td>
                                    <td><span class="estado">Ejemplo</span></td>
                                </tr>
                                <tr>
                                    <td>Barbero</td>
                                    <td>Consulta de agenda y citas asignadas</td>
                                    <td><span class="estado">Ejemplo</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <p class="nota">
                        Esta pantalla no crea cuentas ni aplica permisos reales.
                        La autenticación deberá implementarse de forma segura.
                    </p>
                </div>
            </section>

            <footer class="pie">
                Peluquería y Barbería Don Juan · Maqueta académica
            </footer>
        </main>
    </div>

    <script>
        // Navegación entre las pantallas de la maqueta.
        const botonesMenu = document.querySelectorAll(".enlace-menu");
        const paginas = document.querySelectorAll(".pagina");
        const mensaje = document.getElementById("mensaje");

        botonesMenu.forEach(function(boton) {
            boton.addEventListener("click", function() {
                const destino = boton.dataset.pagina;

                paginas.forEach(function(pagina) {
                    pagina.classList.remove("activa");
                });

                botonesMenu.forEach(function(item) {
                    item.classList.remove("activo");
                });

                document.getElementById(destino).classList.add("activa");
                boton.classList.add("activo");

                window.scrollTo({ top: 0, behavior: "smooth" });
            });
        });

        function mostrarMensaje(texto) {
            mensaje.textContent = texto;
            mensaje.style.display = "block";
        }

        // Registro de citas de demostración.
        const formCita = document.getElementById("formCita");

        formCita.addEventListener("submit", function(evento) {
            evento.preventDefault();

            const cliente = document.getElementById("clienteCita").value.trim();
            const servicio = document.getElementById("servicioCita").value;
            const fecha = document.getElementById("fechaCita").value;
            const hora = document.getElementById("horaCita").value;

            if (!cliente || !servicio || !fecha || !hora) {
                mostrarMensaje("Completa todos los campos de la cita.");
                return;
            }

            const fila = document.createElement("tr");

            [fecha, hora, cliente, servicio].forEach(function(valor) {
                const celda = document.createElement("td");
                celda.textContent = valor;
                fila.appendChild(celda);
            });

            const celdaEstado = document.createElement("td");
            const estado = document.createElement("span");
            estado.className = "estado estado-pendiente";
            estado.textContent = "Pendiente";
            celdaEstado.appendChild(estado);
            fila.appendChild(celdaEstado);

            document.getElementById("tablaCitas").appendChild(fila);

            const total = document.getElementById("totalCitas");
            total.textContent = Number(total.textContent) + 1;
            document.getElementById("reporteCitas").textContent = total.textContent;

            formCita.reset();
            mostrarMensaje("Cita de ejemplo agregada a la tabla.");
        });

        // Registro de clientes de demostración.
        const formCliente = document.getElementById("formCliente");

        formCliente.addEventListener("submit", function(evento) {
            evento.preventDefault();

            const nombre = document.getElementById("nombreCliente").value.trim();
            const telefono = document.getElementById("telefonoCliente").value.trim();

            if (!nombre || !telefono) {
                mostrarMensaje("Completa el nombre y el teléfono.");
                return;
            }

            const fila = document.createElement("tr");

            [nombre, telefono].forEach(function(valor) {
                const celda = document.createElement("td");
                celda.textContent = valor;
                fila.appendChild(celda);
            });

            document.getElementById("tablaClientes").appendChild(fila);

            const total = document.getElementById("totalClientes");
            total.textContent = Number(total.textContent) + 1;

            formCliente.reset();
            mostrarMensaje("Cliente de ejemplo agregado a la tabla.");
        });

        // Búsqueda visual de clientes.
        document.getElementById("buscarCliente").addEventListener("input", function() {
            const busqueda = this.value.toLowerCase();

            document.querySelectorAll("#tablaClientes tr").forEach(function(fila) {
                fila.style.display = fila.textContent.toLowerCase().includes(busqueda)
                    ? ""
                    : "none";
            });
        });

        // Registro de pagos de demostración.
        document.getElementById("formPago").addEventListener("submit", function(evento) {
            evento.preventDefault();

            const cliente = document.getElementById("clientePago").value.trim();
            const valor = Number(document.getElementById("valorPago").value);
            const fecha = document.getElementById("fechaPago").value;
            const metodo = document.getElementById("metodoPago").value;

            if (!cliente || valor <= 0 || !fecha || !metodo) {
                mostrarMensaje("Revisa los datos del pago.");
                return;
            }

            const fila = document.createElement("tr");
            const valores = [
                cliente,
                new Intl.NumberFormat("es-CO", {
                    style: "currency",
                    currency: "COP",
                    maximumFractionDigits: 0
                }).format(valor),
                fecha,
                metodo
            ];

            valores.forEach(function(valorCelda) {
                const celda = document.createElement("td");
                celda.textContent = valorCelda;
                fila.appendChild(celda);
            });

            document.getElementById("tablaPagos").appendChild(fila);
            this.reset();
            mostrarMensaje("Pago de ejemplo agregado a la tabla. No se realizó ninguna transacción.");
        });

        // Validación sencilla de las fechas de consulta.
        document.getElementById("formReporte").addEventListener("submit", function(evento) {
            evento.preventDefault();

            const inicio = document.getElementById("fechaInicio").value;
            const fin = document.getElementById("fechaFin").value;

            if (inicio && fin && inicio > fin) {
                mostrarMensaje("La fecha inicial no puede ser posterior a la fecha final.");
                return;
            }

            mostrarMensaje("Filtros revisados. Los reportes reales requieren una fuente de datos.");
        });
    </script>
</body>
</html>
