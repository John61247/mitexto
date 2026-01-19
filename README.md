public class Lista {
    private int elem[];
    private int cantElem;
    private int max;

    public Lista(int max) {
        this.max = max;
        this.elem = new int[max];
        this.cantElem = 0;
    }
    public void add(int x) {
        if (cantElem < max) {
            this.elem[this.cantElem] = x;
            this.cantElem++;
        }
    }

    public boolean vacia() {
        return cantElem == 0;
    }

    @Override
    public String toString() {
        String s = "[";
        for (int i = 0; i < cantElem; i++) {
            s += elem[i];
            if (i < cantElem - 1) s += ", ";
        }
        return s + "]";
    }

    // ========== INSERTAR ==========
//1
    public void insertarPrim(int x) {
        insertarIesimo(x, 0);
    }

    public void insertarUlt(int x) {
        insertarIesimo(x, cantElem);
    }
//2
    public void insertarIesimo(int x, int i) {
        if (i < 0 || i > cantElem || cantElem >= max) return;
        for (int k = cantElem - 1; k >= i; k--) elem[k + 1] = elem[k];
        elem[i] = x;
        cantElem++;
    } 
//3
    public void insertarAsc(int x) {
        int i = 0;
        while (i < cantElem && elem[i] < x) i++;
        insertarIesimo(x, i);
    }
//4
    public void insertarDesc(int x) {
        int i = 0;
        while (i < cantElem && elem[i] > x) i++;
        insertarIesimo(x, i);
    }
//5
    public void insertarDespuesDe(int x, int nuevoValor) {
        int i = 0;
        while (i < cantElem && elem[i] != x) i++;
        if (i < cantElem) insertarIesimo(nuevoValor, i + 1);
    }
//6 Extra
    public void insertarParImpar(int x) {
        if (x % 2 == 0) insertarPrim(x);
        else insertarUlt(x);
    }

    // ========== ELIMINAR ==========
//1
    private void eliminarNodo(int i) {
        if (i < 0 || i >= cantElem) return;
        for (int k = i; k < cantElem - 1; k++) elem[k] = elem[k + 1];
        cantElem--;
    }

    public void eliminarPrim() {
        if (!vacia()) eliminarNodo(0);
    }

    public void eliminarUlt() {
        if (!vacia()) eliminarNodo(cantElem - 1);
    }
//2
    public void eliminarIesimo(int i) {
        if (i == 0) eliminarPrim();
        else if (i == cantElem - 1) eliminarUlt();
        else eliminarNodo(i);
    }
//3
    public void eliminarRango(int a, int b) {
        if (a < 0) a = 0;
        if (b >= cantElem) b = cantElem - 1;
        for (int i = b; i >= a; i--) eliminarNodo(i);
    }
//4
    public void eliminarImpares() {
        for (int i = cantElem - 1; i >= 0; i--) {
            if (elem[i] % 2 != 0) eliminarNodo(i);
        }
    }
//5
    public void eliminarMayoresQue(int x) {
        for (int i = cantElem - 1; i >= 0; i--) {
            if (elem[i] > x) eliminarNodo(i);
        }
    }
//6 Extra
    public void eliminarEntre(int a, int b) {
        for (int i = cantElem - 1; i >= 0; i--) {
            if (elem[i] > a && elem[i] < b) eliminarNodo(i);
        }
    }
}

public static void main(String[] args) {

        Lista L = new Lista(20);

        // ===== CARGA INICIAL =====
        L.add(10);
        L.add(20);
        L.add(30);
        L.add(40);
        L.add(50);

        System.out.println("Lista inicial:");
        System.out.println(L);
        // ===== INSERTAR =====

        L.insertarPrim(5);
        System.out.println("Despues de insertarPrim(5):");
        System.out.println(L);

        L.insertarUlt(60);
        System.out.println("Despues de insertarUlt(60):");
        System.out.println(L);

        L.insertarIesimo(25, 3);
        System.out.println("Despues de insertarIesimo(25, 3):");
        System.out.println(L);

        L.insertarAsc(35);
        System.out.println("Despues de insertarAsc(35):");
        System.out.println(L);

        L.insertarDespuesDe(20, 22);
        System.out.println("Despues de insertarDespuesDe(20, 22):");
        System.out.println(L);

        // ===== ELIMINAR =====

        L.eliminarPrim();
        System.out.println("Despues de eliminarPrim():");
        System.out.println(L);

        L.eliminarUlt();
        System.out.println("Despues de eliminarUlt():");
        System.out.println(L);

        L.eliminarIesimo(2);
        System.out.println("Despues de eliminarIesimo(2):");
        System.out.println(L);

        L.eliminarImpares();
        System.out.println("Despues de eliminarImpares():");
        System.out.println(L);

        L.eliminarMayoresQue(30);
        System.out.println("Despues de eliminarMayoresQue(30):");
        System.out.println(L);
    }
}
