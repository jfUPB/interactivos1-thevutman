#### Esta es la solucion de mi actividad ✍️
---

``` js
let port;
let connectBtn;

let x;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    fill('white');
    circle(50,50,50);
  
    x = 20
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            x = x+20
            translate(x, 0);
        }
        else if(dataRx == 'B'){
            x = x - 20
            translate(x, 0);
        }
      background(220);
      fill('white');
      circle(50,50,50);
    }


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('h');
}
```

#### Explicación del Funcionamiento

#### Mapeo de los Botones a la Posición del Círculo  
- El micro:bit detecta cuando los botones son presionados.  
- Si el botón A es presionado, el micro:bit envía la letra 'A'.  
- Si el botón B es presionado, el micro:bit envía la letra 'B'.  
- p5.js recibe estos datos y actualiza la posición del círculo en la pantalla.  
- `port.read(1)` lee los datos enviados por el micro:bit.  
- Dependiendo del dato recibido ('A' o 'B'), se ajusta la posición del círculo.  

---

#### Resultados Observados  
- El círculo se mueve a la izquierda al presionar el botón B y a la derecha al presionar el botón A.  
- La interfaz de p5.js permite la conexión y desconexión del micro:bit con un botón.  
- Se mantiene la comunicación en serie entre el micro:bit y p5.js para actualizar la posición del círculo en tiempo real.  
