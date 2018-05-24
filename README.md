# kerneldbg

desde un host linux, vamos a configurar dos vmware virtual machines con windows 7 para que una debuggee a la otra

las maquinas virtuales van a ser llamadas "guest debugee" que va a ser el windows 7 a debuggearle el ring0

y la "guest dbg" que va a correr el debugger WinDBG

## guest dbg
esta se tiene que hacer primero porque va a ser la que va a crear el pipe de comunicacion con la maquina debuggeada

creamos un windows 7 limpio con vmware y despues le aNIadimos un puerto serie con el siguiente formato

![alt text](https://github.com/lupulabs/kerneldbg/blob/master/img/confdebugee.png)

el pipe lo va a pasar al host a traves de /tmp/kdpipe:
* el modo server quiere decir, que esta maquina lo va a crear cuando arranque.
* lo de Virtual Machine es para decirle que es para comunicarse con otra vm.

ahora cuando arranquemos esta maquina en tmp vamos a tener el serial emulado en el host

![alt text](https://github.com/lupulabs/kerneldbg/blob/master/img/kdpipe.png)

## guest debugee
este va a ser el que le vamos a inspeccionar las tripas

instalamos un win 7 fresco igual que antes, pero ahora configuramos el puerto serial asi

![alt text](https://github.com/lupulabs/kerneldbg/blob/master/img/confdbg.png)

ahora le decimos que:
* se conecte como cliente al /tmp/kdpipe (que ya va a estar creado por el server)

y en ambas maquinas le ponemos "Connect at power on" para que este disponible ni bien arrancan

## side channel, o probando el serial
lo primero que tenemos que tener es comunicacion serial entre las dos maquinas, para probarlo yo instale putty en ambas maquinas y arranco el "guest dbg" que hace el pipe y despues el "guest debugge" que consume ese archivo

desde ambas maquinas configuramos putty para que trabaje asi:
![alt text](https://github.com/lupulabs/kerneldbg/blob/master/img/putty.png)

* COM2 es seteado porque vimos que vmware nos puso Serial Port 2 al que creamos.
* 115200 es el baudrate que definimos igual en ambas maquinas para que se entiendan
* y Serial porque queremos que se comuniquen por este pseudo puerto para activar el debugger remoto


