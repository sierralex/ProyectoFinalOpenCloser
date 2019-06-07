# ProyectoFinalOpenCloser
Proyecto Final
Este proyecto es el open closer para realizar un mini blockchain, el cual permite realizar lo siguiente

1. Consultar transacciones
2. Validar el ingreso de 3 transacciones por bloque
3. Mostrar el Hash del bloque

Este desarrollo es una colaboracion con varios grupos y entregar un producto final el cual cuenta con:
Metodo 


### Pre-requisitos 📋

Para realizar esta practica se debe contar con todos los modulos los cuales son:

- Blockchain
- Wallet
- OpenCloser
- Register 


##### Instalación 🔧
El programa contara con un temporizador el cual esta configurado en un milisegundo 
```namespace OpenCloser.Controllers
{
    public class ValuesController : ApiController
    {
        public static Timer t = new Timer(Metodo2, null, 0, 1000);

```
Se crea el Metodo2 el cual nos ayudara asolicitar desde la url para que nos traiga la informacion de esta y poderla validar con la aplicacion
```
private static void Metodo2(object state)
        {
            Metodo();
        }

        [System.Web.Http.AcceptVerbs("GET", "POST")]
        [System.Web.Http.HttpGet, System.Web.Http.HttpPost]
        private static JsonResult Metodo()
        {
            string resp = "";

            HttpWebRequest request = WebRequest.Create("https://api.etherscan.io/api?module=block&action=getblockreward&blockno=2165403&apikey=V7Q5WWCFZWJP18SE9Z7U8C7C5NJDHHT7YC") as HttpWebRequest;
            request.Method = "POST";
            //request.ContentType = "application/x-www-form-urlencoded"; //"application/json; charset=utf-8";
            //request.Headers.Add("module", "block");
            //request.Headers.Add("action", "getblockreward");
            //request.Headers.Add("blockno", "2165403");
            //request.Headers.Add("apikey", "V7Q5WWCFZWJP18SE9Z7U8C7C5NJDHHT7YC");
            request.ContentLength = 0;

            HttpWebResponse response = request.GetResponse() as HttpWebResponse;
            StreamReader reader = new StreamReader(response.GetResponseStream());
            
```
Metodos de generar hash el cual calcula un hash apartir del string, luego realiza la conversion a hexadecimal y lo retorna
```

   // Primeiro passo, calcular o MD5 hash a partir da string
            SHA256 sha256 = System.Security.Cryptography.SHA256.Create();
            byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(textHash);
            byte[] hash = sha256.ComputeHash(inputBytes);

            // Segundo passo, converter o array de bytes em uma string haxadecimal
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < hash.Length; i++)
            {
                sb.Append(hash[i].ToString("X2"));
            }
            return sb.ToString();

            //var msg = Encoding.ASCII.GetBytes(textHash);
            //var sha = new SHA256Managed();
            //var hash = sha.ComputeHash(msg);
            //string nuevoHash = "";
            //foreach (char b in hash)
            //{
            //    nuevoHash += b.ToString();
            //}


```
En esta parte recibimos 3 parametros el cual los concatena y pasa al metodo generar hash, donde valida que tenga los cuatro ceros iniciales, si este no los contiene este se vulve a concatenar hasta que cumpla los parametros 
```
        [System.Web.Http.AcceptVerbs("GET", "POST")]
        //[HttpGet]
        public JsonResult ObtenerInfoBloque(string idBloque, string data, string hashPreview)
        {
            int nouse = 0;
            Boolean hashValido = false;
            string nuevoHash = "";

            while ( hashValido == false) { 
                
                string textHash = idBloque + nouse + data + hashPreview;
                nuevoHash = GenerarHash(textHash);

                String primerosCeros = nuevoHash.Substring(0, 4);

                if( primerosCeros == "0000")
                {
                    hashValido = true;
                }
                nouse ++;
            }

           return new JsonResult() { Data = nuevoHash, JsonRequestBehavior = JsonRequestBehavior.AllowGet }; 

        }

```
## Construido con 🛠️

* Visual studio - Programa en el cual se desarrollo
* [Url](https://api.etherscan.io/api?module=block&action=getblockreward&blockno=2165403&apikey=V7Q5WWCFZWJP18SE9Z7U8C7C5NJDHHT7YC) - Utilizo esta api con el fin de validar el funcionamiento

## Wiki 📖

Puedes encontrar mucho más de cómo utilizar este proyecto en nuestra [Wiki](https://github.com/https://github.com/sierralex/ProyectoFinalOpenCloser//wiki)


## Autores ✒️


* **Brayan Salas** - *Trabajo Inicial* - [bsalas](https://github.com/villanuevand)
* **David Vigues** - *Documentación y trabajo inicial* - [dvilgues](https://github.com/dvilgues)
* **Alexander Sierra** - *Trabajo inicialn* - [sierralex](https://github.com/sierralex)
* **Juan Sanchez** - *Documentación* - [jsanche](https://github.com/jsanche)
* **Greys leon** - *Documentación* - [gleon](https://github.com/gleon)

## Expresiones de Gratitud 🎁

* Comenta a otros sobre este proyecto  talvez les pueda interesar 📢
* Invita una cerveza 🍺 a alguien del equipo con el fin de platicar. 
* Da las gracias públicamente 🤓 para animarnos a subir muchisimos mas :).
* etc.



