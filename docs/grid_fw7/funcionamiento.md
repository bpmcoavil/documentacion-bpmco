---
sidebar_position: 1
title: Funcionamiento Grid Framework7
slug: /funcionamiento_grid_framework7
toc_max_heading_level: 4
---

:::info 
_**Author:** Cristian Camilo Cantillo_
:::

## Grafico

```ciclo de vida```

```
    ○
    │
    ├──► Inicialización
    │       │
    │       ├────► HTML
    │       │       │
    │       │       ├──► Tabla HTML con la estructura de fw7.
    │       │       └──► Popup Fw7 con estructura par el formulario de entrada.
    │       │  
    │       └────► Javascript
    │               │
    │               ├──► Objeto para manipular la grid.  
    │               ├──► Objeto con la configuración de las columnas de la grid.
    │               └──► Objeto que asocia la grid con su configuración.
    │
    │
    ├──► Renderizado
    │       │
    │       ├──► Cargue Inicial.
    │       │
    │       └──► Actualización Dinámica.
    │
    │
    ├──► Interacción Usuario
    │       │
    │       ├──► Eventos.
    │       │
    │       └──► Responsibidad.
    │
    │
    └──► Actualización
            │
            ├──► Cambios Contenido.
            │
            └──► Re-renderizado.
    
```

---

## Video Explicación

<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/MUe_ngkd1Xc"
  title="Explicación Grid Framework7"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>

---

## Inicialización

```configuración grid framework7```

### HTML

#### Tabla HTML con estructura fw7

Las tablas de Fw7 tienen la ventaja de verse muy bien en celulares, es muy responsive, pero carece de funcionalidad, con el script de htmlGrid se le agrega interacción y se extienden las opciones.

```html title="Tabla"
<div class="card data-table data-table-collapsible data-table-init">
    <div class="card-header">
        <div class="data-table-title">
            Encabezado de la tabla
        </div>
    </div>
    <div class="card-content">
        <table class="table" id="gPruebas">
            <thead>
                <tr>
                    <th class="label-cell">Nombre</th>
                    <th class="label-cell">Apellido</th>
                    <th class="label-cell">Edad</th>
                    <th class="label-cell">Salario</th>
                    <th class="label-cell">Estado</th>
                    <th class="label-cell">Opc</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>
        <input type="hidden" id="_tgPruebas" />
    </div>
</div>

```

#### Popup Fw7 con estructura par el formulario de entrada

Toda la entrada de datos para la grid se hace a través de este componente, allí deben estar los campos que cargar y guardan la información en la tabla fw7, es necesario que el id del popup sea el mismo id de la grid pero empezando con raya baja _.

```html title="PopUp"
<div class="popup" id="_gPruebas" style="display: none;">
    <div class="page">
        <div class="navbar">
            <div class="navbar-inner">
                <div class="navbar-bg"></div>
                <div class="title">Datos de Pruebas</div>
                <div class="right">
                    <a href="#" class="link popup-close">
                        <i class="material-icons md-only">close</i>
                    </a>
                </div>
            </div>
        </div>
        <div class="page-content">
            <div class="row">
                <div class="large-50 medium-50 col-100 list">
                    <div class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-label">Nombre</div>
                            <div class="item-input-wrap">
                                <input type="text" id="_t1" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="large-50 medium-50 col-100 list">
                    <div class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-label">Apellido</div>
                            <div class="item-input-wrap">
                                <input type="text" id="_t2" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="large-50 medium-50 col-100 list">
                    <div class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-label">Edad</div>
                            <div class="item-input-wrap">
                                <input type="text" id="_t3" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="large-50 medium-50 col-100 list">
                    <div class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-label">Salario</div>
                            <div class="item-input-wrap">
                                <input type="text" id="_t4" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="large-50 medium-50 col-100 list">
                    <div class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-label">Estado</div>
                            <div class="item-input-wrap">
                                <a class="item-link smart-select smart-select-init" data-open-in="popup"
                                    data-searchbar="true"  data-searchbar-placeholder="Buscar">
                                    <select id="_s1" name="_s1" class="ssVal" data-idt="_t_s1">
                                        <option value="" >Seleccione Estado</option>
                                        <option value="Activo" >Activo</option>
                                        <option value="Retirado">Retirado</option>
                                        <option value="Vacaciones">Vacaciones</option>
                                    </select>
                                    <div class="item-content">
                                        <div class="item-inner">
                                            <div class="item-title nb-hidden">Estado</div>
                                        </div>
                                    </div>
                                </a>
                                <input type="hidden" id="_t_s1" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row btn-modal">
                <div class="large-20 medium-20 col-0"></div>
                <div class="large-60 medium-60 col-100 list btnSavegPruebas">
                    <button type="button" class="col button button-fill button-round">Aceptar</button>
                </div>
                <div class="large-20 medium-20 col-0"></div>
            </div>
        </div>
    </div>
</div>
```

### Javascript

#### Objeto para manipular la grid

Simplemente es una variable global que va a manejar la interacción y la lógica relacionada con la grid, usualmente se declara con el mismo id que se le puso a la tabla en el HTML.

```js title="Objeto Grid"
var gPruebas = null;
```

#### Objeto de configuración

```js title="Objeto Configuracipon Grid"
var gPruebasConf = {
    Nombre: { req: true, id: '_t1', idx: 0, vDef: '', ver: true, verModal: true },
    Apellido: { req: true, id: '_t2', idx: 1, vDef: '', ver: true, verModal: true },
    Edad: { req: true, id: '_t3', idx: 2, vDef: '', ver: true, verModal: true },
    Salario: { req: true, id: '_t4', idx: 3, vDef: '', ver: true, verModal: true },
    Estado: { req: true, id: '_s1', idx: 4, vDef: '', ver: true, verModal: true },
    Opc: { req: false, id: '', idx: 5, vDef: '', ver: true, verModal: false }
};

var optAdd = "<i class='material-icons pointer iPopup' data-tipo='add'>add_circle_outline</i>";
var optDel = "<i class='material-icons pointer iPopup' data-tipo='delete'>remove_circle_outline</i>";
var iOpts = optAdd + optDel;
```

| Propiedad | tipo    | Descripción                                                        |
| --------- | ------- | ------------------------------------------------------------------ |
| req       | boolean | Indica si el campo es requerido                                    |
| id        | string  | Id del campo en el popup que está asociado a la columna            |
| idx       | integer | Índice de la columna, debe corresponder a la posición en el HTML   |
| vDef      | string  | Valor por defecto de la columna                                    |
| ver       | boolean | Indica si la columna se va a mostrar en la tabla                   |
| verModal  | boolean | Indica si el campo se debe mostrar en el popup                     |
| min       | integer | Para la validación, si el campo debe tener un mínimo de caracteres |
| max       | integer | Para la validación, si el campo debe tener un máximo de caracteres |
| regExp    | Regula  | Exp	Una expresión regular, por ejemplo alfanumérico /^[A-Za-z0-9]/ |

#### Objeto de asociación

Este es el objeto que agrupa las grids y asocia el objeto inicializado con su configuración.

Las llaves del objeto es el id de cada grid, el objeto de la grid ya debe estar inicializado.

```js title="Objeto de asociación"
var objGrids = {};

objGrids['gPruebas'] = { 'grid': gPruebas, 'conf': gPruebasConf };
objGrids['gInventario'] = { 'grid': gInventario, 'conf': gInventarioConf };
```
---

Prueba abcs 123

---

## Ultima Actualización

<div class="ultima-actualizacion">
  <small>
    <i>
      Ultima actualización:
      <b> 13 de septiembre de 2024.</b>
    </i>
  </small>

  <small>
    <i>
      Actualizado por:
      <b> Julian A. Ortiz.</b>
    </i>
  </small>
</div>
