# mini-juego-
#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct Tarea {
    string descripcion;
    bool completada;
    string prioridad; // Alta, Media, Baja
};

void agregarTarea(vector<Tarea>& tareas);
void mostrarTareas(const vector<Tarea>& tareas);
void completarTarea(vector<Tarea>& tareas);

int main() {
    vector<Tarea> tareas;
    int opcion = 0;

    while (opcion != 4) {
        cout << "\nLISTA DE TAREAS\n\n";
        cout << "1. Agregar tarea\n";
        cout << "2. Mostrar tareas\n";
        cout << "3. Marcar tarea como completada\n";
        cout << "4. Salir\n\n";
        cout << "Seleccione una opción: ";

        if (!(cin >> opcion)) {
            cin.clear();
            cin.ignore(1000, '\n');
            cout << "Opción no válida.\n";
            continue;
        }
        cin.ignore();

        switch (opcion) {
            case 1:
                agregarTarea(tareas);
                break;
            case 2:
                mostrarTareas(tareas);
                break;
            case 3:
                completarTarea(tareas);
                break;
            case 4:
                cout << "Saliendo del programa...\n";
                break;
            default:
                cout << "Opción no válida.\n";
                break;
        }
    }

    return 0;
}

void agregarTarea(vector<Tarea>& tareas) {
    Tarea nuevaTarea;
    cout << "Ingrese la tarea: ";
    getline(cin, nuevaTarea.descripcion);
    
    int opcPrioridad = 0;
    cout << "Seleccione la prioridad (1. Alta, 2. Media, 3. Baja): ";
    cin >> opcPrioridad;
    cin.ignore();

    switch (opcPrioridad) {
        case 1: nuevaTarea.prioridad = "Alta"; break;
        case 2: nuevaTarea.prioridad = "Media"; break;
        case 3: nuevaTarea.prioridad = "Baja"; break;
        default: nuevaTarea.prioridad = "Media"; break;
    }

    nuevaTarea.completada = false;
    tareas.push_back(nuevaTarea);
    cout << "Tarea agregada correctamente.\n";
}

void mostrarTareas(const vector<Tarea>& tareas) {
    if (tareas.empty()) {
        cout << "\nNo hay tareas en la lista.\n";
        return;
    }
    cout << "\nTAREAS\n";
    for (size_t i = 0; i < tareas.size(); ++i) {
        string estado = tareas[i].completada ? "Completada" : "Pendiente";
        cout << (i + 1) << ". [" << estado << "] [" << tareas[i].prioridad << "] " << tareas[i].descripcion << "\n";
    }
}

void completarTarea(vector<Tarea>& tareas) {
    if (tareas.empty()) {
        cout << "\nNo hay tareas registradas para completar.\n";
        return;
    }

    mostrarTareas(tareas);
    cout << "\nSeleccione la tarea: ";
    int indice;
    if (cin >> indice && indice >= 1 && indice <= static_cast<int>(tareas.size())) {
        tareas[indice - 1].completada = true;
        cout << "Tarea marcada como completada.\n";
    } else {
        cout << "Opción no válida.\n";
    }
    cin.ignore();
}
