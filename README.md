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
```
 resp = reader.ReadToEnd();

            return new JsonResult() { Data = resp, JsonRequestBehavior = JsonRequestBehavior.AllowGet };
        }

        // GET api/values
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5
        public string Get(int id)
        {
            return "value" + id;
        }

        // POST api/values
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5
        public void Delete(int id)
        {
        }

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
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)

