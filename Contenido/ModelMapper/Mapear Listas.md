# Mapear Listas

<p align="center">
  <em></em>
</p>

> de esta forma se mapean las listas de un tipo hacia listas de otro tipo
 
 ````java
    public List<Distritos> getAll(){
        //1
        List<DistritosEntity> allDistritos = repository.findAll();
        //2
        Type listType = new TypeToken<List<Distritos>>(){}.getType();
        //3
        return modelMapper.map(allDistritos,listType);
    }
````
> 1) se trae una lista de entities
> 2) se crea un Type que sirve para indicar cual es el tipo de referencia
> 3) el model mapper mapea una lista de entities a una lista indicada por el tipo en el paso 2
