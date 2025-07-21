using System;
using System.Collections.Generic;

namespace ParqueDiversiones
{
    class Persona
    {
        public string Nombre { get; set; }
        public int NumeroTurno { get; set; }

        public Persona(string nombre, int turno)
        {
            Nombre = nombre;
            NumeroTurno = turno;
        }

        public override string ToString()
        {
            return $"Turno {NumeroTurno}: {Nombre}";
        }
    }

    class Atraccion
    {
        private Queue<Persona> cola;
        private int capacidadMaxima;
        private int contador;

        public Atraccion(int capacidad)
        {
            cola = new Queue<Persona>();
            capacidadMaxima = capacidad;
            contador = 1;
        }

        public string RegistrarPersona(string nombre)
        {
            if (cola.Count >= capacidadMaxima)
            {
                return $"⛔ Asientos llenos. {nombre} no puede ingresar.";
            }
            else
            {
                Persona persona = new Persona(nombre, contador++);
                cola.Enqueue(persona);
                return $"✅ {nombre} registrado con éxito.";
            }
        }

        public void MostrarReporte()
        {
            Console.WriteLine("📋 Lista de personas registradas:");
            foreach (Persona p in cola)
            {
                Console.WriteLine(p.ToString());
            }
            Console.WriteLine($"Total registrados: {cola.Count}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            Atraccion atraccion = new Atraccion(30);
            string opcion;

            do
            {
                Console.WriteLine("\n--- Menú ---");
                Console.WriteLine("1. Registrar persona");
                Console.WriteLine("2. Ver reporte");
                Console.WriteLine("3. Salir");
                Console.Write("Seleccione una opción: ");
                opcion = Console.ReadLine();

                switch (opcion)
                {
                    case "1":
                        Console.Write("Ingrese el nombre de la persona: ");
                        string nombre = Console.ReadLine();
                        Console.WriteLine(atraccion.RegistrarPersona(nombre));
                        break;
                    case "2":
                        atraccion.MostrarReporte();
                        break;
                    case "3":
                        Console.WriteLine("🚪 Saliendo...");
                        break;
                    default:
                        Console.WriteLine("⚠️ Opción no válida.");
                        break;
                }

            } while (opcion != "3");
        }
    }
}
