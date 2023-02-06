# Prog_Web_02200131001_A_2023
Taller 1: Supermercado(Registro y venta de productos).
--------------------------------------------------------------------------------------------------------------------------------------------------------
package Main;

import Clases.Opciones;
import static java.awt.Frame.ICONIFIED;
import java.util.Scanner;

/**
 *
 * @author JoseF
 */
public class Tienda {

    public static void main(String[] args) {
        Opciones producto = new Opciones();
        Scanner sc = new Scanner(System.in);
        System.out.println("-----------------------------------------------------------------------------------------------------");
        System.out.println("Bienvenido a la tienda X!");
        System.out.println("-----------------------------------------------------------------------------------------------------");
        System.out.println("Menú:");
        System.out.println("1. Ingresar producto.");
        System.out.println("2. Listar.");
        System.out.println("2. Vender producto.");
        System.out.println("-----------------------------------------------------------------------------------------------------");
        System.out.print("Seleccione una opción: ");
        String menu = sc.nextLine();
        System.out.println("-----------------------------------------------------------------------------------------------------");
        while ("1".equals(menu) || "2".equals(menu) || "3".equals(menu)) {
            switch (menu) {
                case "1" -> {
                    System.out.println("Ingrese datos del producto: ");
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.print("Nombre: ");
                    String nombre = sc.nextLine();
                    System.out.print("Código: ");
                    String Id = sc.nextLine();
                    System.out.print("Categoría: ");
                    String categoria = sc.nextLine();
                    System.out.print("Descripción: ");
                    String descripcion = sc.nextLine();
                    System.out.print("Precio: ");
                    String Precio = sc.nextLine();
                    System.out.print("Marca: ");
                    String marca = sc.nextLine();
                    int id = Integer.parseInt(Id);
                    int precio = Integer.parseInt(Precio);
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.println(producto.ingresar(id, nombre, marca, descripcion, categoria, precio));
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.print("Seleccione una opción: ");
                    menu = sc.nextLine();
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                }
                case "2" -> {
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.print(producto.listar(ICONIFIED));
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.print("Seleccione una opción: ");
                    menu = sc.nextLine();
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                }
                case "3" -> {
                    System.out.print("Busque el Código del producto que desee vender: ");
                    String Dato = sc.nextLine();
                    int dato = Integer.parseInt(Dato);
                    System.out.println(producto.identificador(dato));
                    System.out.print("Ingrese el identificador del producto para venderlo: ");
                    String Dato1 = sc.nextLine();
                    int dato1 = Integer.parseInt(Dato1);
                    System.out.println(producto.buscarPorIdentificador(dato, dato1));
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                    System.out.print("Seleccione una opción: ");
                    menu = sc.nextLine();
                    System.out.println("-----------------------------------------------------------------------------------------------------");
                }
                default -> {
                }
            }

        }
        System.out.println("Opción errónea.");

    }
}
--------------------------------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------------------------------
package Clases;
import java.util.ArrayList;

/**
 *
 * @author JoseF
 */
public class Opciones {

    private ArrayList<Producto> ProductoTienda;

    public Opciones() {
        this.ProductoTienda = new ArrayList<Producto>();
    }
    //Buscar producto.

    private Producto buscar(int nIdentificador) {
        Producto buscar = null;
        if (!this.ProductoTienda.isEmpty()) {
            for (Producto e : this.ProductoTienda) {
                if (e.codigo==nIdentificador) {
                    buscar = e;
                    return buscar;
                }
            }
        }
        return buscar;
    }

    public String ingresar(int nIdentificador, String nNombre, String nMarca, String nDescripcion, String nCategoria, int nPrecio) {
        Producto xx = this.buscar(nIdentificador);

        if (xx != null) {
            return "El producto ya existe.";
        } else {
            xx = new Producto(nIdentificador, nNombre, nMarca, nDescripcion, nCategoria, nPrecio);
            this.ProductoTienda.add(xx);
            return "Producto registrado.";
        }
    }

    //Buscar prodcuto por codigo.
    public String buscarPorIdentificador(int codigo, int identificador) {
        String cad = "";
        if (!this.ProductoTienda.isEmpty()) {
            for (Producto e : this.ProductoTienda) {
                if (e.getCodigo() == codigo) {
                    cad = cad + "Producto encontrado:" + ProductoTienda.indexOf(e) + "\n" + "Nombre: "
                            + e.getNombre() + "\n" + "Identificador: " + e.getCodigo() + "\n" + "Categoría: "
                            + e.getCategoria() + "\n" + "Precio: " + e.getPrecio() + "$";
                    ProductoTienda.remove(identificador);
                    return "Producto vendido.";
                }
            }
            if (cad.isEmpty()) {
                return "Producto no encontrado.";
            }
            return cad;
        }
        return "Producto no encontrado.";

    }

    public String listar(int identificador) {
        String listado = "";
        if (!this.ProductoTienda.isEmpty()) {
            for (Producto e : this.ProductoTienda) {
                listado = listado + e.toString()+ "\n";
            }
            return listado;
        }
        return "No hay registro de productos.";
    }

    public String identificador(int codigo) {
        String cad = "Prodcuto no encontrado.";
        if (!this.ProductoTienda.isEmpty()) {
            for (Producto e : this.ProductoTienda) {
                if (e.getCodigo() == codigo) {
                    cad = "Identificador del producto:" + ProductoTienda.indexOf(e);
                }
            }
        }
        return cad;
    }

}
--------------------------------------------------------------------------------------------------------------------------------------------------------

--------------------------------------------------------------------------------------------------------------------------------------------------------
package Clases;

/**
 *
 * @author JoseF
 */
public class Producto {

    public int codigo;
    public String nombre;
    public String marca;
    private String descripcion;
    private String categoria;
    public int precio;

    public Producto(int identificador, String nombre, String marca, String descripcion, String categoria, int precio) {
        this.categoria = categoria;
        this.descripcion = descripcion;
        this.codigo = identificador;
        this.marca = marca;
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getNombre() {
        return nombre;
    }

    public int getCodigo() {
        return codigo;
    }

    public String getMarca() {
        return marca;
    }

    public String getDescripcion() {
        return descripcion;
    }

    public String getCategoria() {
        return categoria;
    }

    public int getPrecio() {
        return precio;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public void setMarca(String marca) {
        this.marca = marca;
    }

    public void setDescripcion(String descripcion) {
        this.descripcion = descripcion;
    }

    public void setCategoria(String categoria) {
        this.categoria = categoria;
    }

    public void setCodigo(int codigo) {
        this.codigo = codigo;
    }

    public void setPrecio(int precio) {
        this.precio = precio;
    }

    public String toString() {
        return "Código: " + this.codigo + "\n" + "Nombre: " + this.nombre + "\n"
                + "Descripcion: " + this.descripcion + "\n" + "Categoria: " + this.categoria + "\n"
                + "Precio: " + this.precio + "\n";

    }
}
--------------------------------------------------------------------------------------------------------------------------------------------------------
