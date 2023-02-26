# Lista_Circulares
En este contenido se puede realizar un programa donde agremamos productos a una lista Circular
public class Tarea_Est_Lista_Circular {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ListaCircular lista = new ListaCircular();
        
         Producto producto = null; 
         Producto pro;

        int opcion = 0;
        boolean Salir = false;

        while (opcion != 7)
        {
            System.out.println("------- MENU -------");
            System.out.println("1. Inicializar Lista circular");
            System.out.println("2. Insertar next");
            System.out.println("3. Insertar ANTES");
            System.out.println("4. Borrar elemento");
            System.out.println("5. Buscar( en funcion) ");
            System.out.println("6. Imprimir Lista");
            System.out.println("7. Salir");

            System.out.print("Seleccione una opcion: ");
            System.out.println("");
            System.out.println("");

            opcion = scanner.nextInt();

            switch (opcion)
            {
                case 1:
                    System.out.println("\n Se crea nueva lista");
                   lista.ListaCircular();
                    System.out.println("");

                    break;
                case 2:
                    producto = new Producto(0, "", 0);
                    System.out.println("Ingrese el codigo del producto: ");
                    producto.setCodigo(scanner.nextInt());
                    System.out.println("Ingrese la descripcion del producto: ");
                    producto.setDescripcion(scanner.next());
                    System.out.println("Ingrese el precio del producto: ");
                    producto.setPrecio(scanner.nextInt());
                    
                    lista.ingresar(producto);
                    System.out.println("");

                    break;
                case 3:
                    producto = new Producto(0, "", 0);
                    System.out.println("Ingrese el codigo del producto: ");
                    producto.setCodigo(scanner.nextInt());
                    System.out.println("Ingrese la descripcion del producto: ");
                    producto.setDescripcion(scanner.next());
                    System.out.println("Ingrese el precio del producto: ");
                    producto.setPrecio(scanner.nextInt());
                    lista.ingresarAntes(producto);
                    System.out.println("");
                   
                    break;
                case 4:
                   
                    pro = new Producto(0, "", 0);
                    System.out.println("Lista antes de eliminar un producto:");
                    lista.verListaCircular();
                    System.out.println("");
                    System.out.println("Ingrese el código del producto que desea eliminar:");                   
                    pro.setCodigo(scanner.nextInt());                 
                    scanner.nextLine();
                    System.out.println("Ingrese la descripción del producto que desea eliminar:");
                    pro.setDescripcion(scanner.next());
                    System.out.println("Ingrese el precio del producto que desea eliminar: ");
                    pro.setPrecio(scanner.nextInt());
                                                         
                    lista.eliminar2(pro);
                    
                    break;
                case 5:
                    System.out.println("Insertar el elemento que desea buscar: ");
                    producto.setCodigo(scanner.nextInt());
                    lista.buscarCircular(producto);
                    break;
                case 6:
                    System.out.println("\nLista completa: ");
                    lista.verListaCircular();
                    break;
                case 7:
                     Salir = true;

                    break;
                default:
                    System.out.println("Opción inválida. Por favor, seleccione una opción válida.");
                    break;
            }

        }

    }

    }


//CLASE ListaCircular------------------------------------------------------------------------------------------------------------------------

public class ListaCircular {
Scanner scanner = new Scanner(System.in);
    nodoListaCircular primero;
    nodoListaCircular ultimo;

    public void ListaCircular() {
        primero = null;
        ultimo = null;
    }
    public void ingresar(Producto producto){
        nodoListaCircular nuevo = new nodoListaCircular();
        nuevo.producto = producto;
       
        if (primero == null){
            primero = nuevo;
            ultimo = primero;
            primero.siguiente = ultimo;
        }else{
            ultimo.siguiente = nuevo;
            nuevo.siguiente = (nodoListaCircular) primero;
            ultimo = nuevo;
        }
    }
    public void ingresarAntes(Producto producto){
        nodoListaCircular nuevo = new nodoListaCircular();
        nuevo.producto = producto;
       
        if (primero == null){
            primero = nuevo;
            ultimo = primero;
            primero.siguiente = ultimo;
           
        }else{
            nuevo.siguiente = primero;
            primero = nuevo;
            ultimo.siguiente = (nodoListaCircular) primero;
            
        }
    }
  
  public void verListaCircular(){
        nodoListaCircular actual = new nodoListaCircular();
        actual = (nodoListaCircular) primero;
        do {
            System.out.println(" "+actual.producto.toString());                
            actual = actual.siguiente;
        }while (actual != primero);
    }
  
  
  public boolean buscarCircular(Producto x){
        nodoListaCircular actual = new nodoListaCircular();
        actual = primero;
        boolean encontrado = false;
        do {
            if (actual.producto == x){
                encontrado = true;
                System.out.println("El producto "+"Codigo:  " + x.getCodigo() +"Descripcion: "+ x.getDescripcion()+ "Precio:  "+x.getPrecio()+ ", fue encontrado.");
            }            
            actual = actual.siguiente;
        }while (actual != primero);
        if (encontrado == true){
            System.out.println("encontrado");
        }else
        {
           System.out.println("no existe"); 
        }
        return encontrado;
    }
   

  
  public void modificarProducto(int codigo, String nuevaDescripcion, int nuevoPrecio) {
    nodoListaCircular actual = primero;
    boolean encontrado = false;
    do {
        if (actual.producto.getCodigo() == codigo) {
            actual.producto.setDescripcion(nuevaDescripcion);
            actual.producto.setPrecio(nuevoPrecio);
            encontrado = true;
        }
        actual = actual.siguiente;
    } while (actual != primero && !encontrado);
    if (encontrado) {
        System.out.println("Producto modificado exitosamente");
    } else {
        System.out.println("El producto no se encuentra en la lista");
    }
}
  
   
  
   public void eliminar(Producto producto){
        nodoListaCircular actual = new nodoListaCircular();
        nodoListaCircular anterior = new nodoListaCircular();
        actual = primero;
        anterior = ultimo;        
        do{
            if (actual.producto == producto){
              if (actual == primero){
                    primero = primero.siguiente;
                    ultimo.siguiente = primero;
                }else{
                  if (actual == ultimo){
                      anterior.siguiente = ultimo.siguiente;
                      ultimo = anterior;
                  }else{
                      anterior.siguiente = actual.siguiente;
                  }
              }  
            } 
             anterior = actual;
             actual = actual.siguiente;        
        }while (actual != primero);  
    } 
   
   public void eliminar2(Producto producto) {
    if (primero == null) {
        return; // La lista está vacía
    }
    nodoListaCircular actual = primero;
    nodoListaCircular anterior = null;
    do {
        if (actual.producto.equals(producto)) {
            if (actual == primero) {
                primero = primero.siguiente;
                ultimo.siguiente = primero;
            } else if (actual == ultimo) {
                anterior.siguiente = primero;
                ultimo = anterior;
            } else {
                anterior.siguiente = actual.siguiente;
            }
            return; // Se encontró y eliminó el elemento
        }
        anterior = actual;
        actual = actual.siguiente;
    } while (actual != primero);
}
    
}

//CLASE Producto_------------------------------------------------------------------------

public class Producto {
    
    private int codigo;
    private String descripcion;
    private int precio;

    public Producto(int Codigo, String Descripcion, int Precio) {
        this.codigo = Codigo;
        this.descripcion = Descripcion;
        this.precio = Precio;
    }

    public int getCodigo() {
        return codigo;
    }

    

    public void setCodigo(int codigo) {
        this.codigo = codigo;
    }

    public String getDescripcion() {
        return descripcion;
    }

    public void setDescripcion(String descripcion) {
        this.descripcion = descripcion;
    }

    public int getPrecio() {
        return precio;
    }

    public void setPrecio(int precio) {
        this.precio = precio;
    }

   
    @Override
    public String toString() {
        return "\n"+ " Producto " +"\n" + "codigo=  " + codigo +"\n"+"\n"+ "descripcion=  " + descripcion +"\n"+ "precio=  "+ precio + "";
    }
}

//CLASE nodoListaCircular

public class nodoListaCircular {
    Producto producto;
    nodoListaCircular siguiente;

}
