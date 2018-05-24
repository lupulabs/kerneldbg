# kerneldbg

desde un host linux, vamos a configurar dos vmware virtual machines con windows 7 para que una debuggee a la otra

las maquinas virtuales van a ser llamadas "guest debugee" que va a ser el windows 7 a debuggearle el ring0

y la "guest dbg" que va a correr el debugger WinDBG

## guest dbg
esta se tiene que hacer primero porque va a ser la que va a crear el pipe de comunicacion con la maquina debuggeada

creamos un windows 7 limpio con vmware y despues le aNIadimos un puerto serie con el siguiente formato

!(img/confdebugee.png)
