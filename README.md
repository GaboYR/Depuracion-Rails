# Depuracion-Rails
Para corregir los errores como **"undefined method 'title' for nil:NilClass"**, debemos garantizar la validación de los objetos antes de intentar acceder a sus atributos en la vista.
En este caso: 
```ruby
def show
  id = params[:id] # retrieve movie ID from URI route
  @movie = Movie.find(id) # look up movie by unique ID
  # will render render app/views/movies/show.html.haml by default
  if @movie.nil?
    # Manejar el caso en que la pelicula no se encuentre
  end
end
```
## Detencion de la ejecución dentro de un método de un controlador
Detien la ejecución dentro de un método de un controlador lanzando una excepción cuyo mensaje sea una representación del valor que quieres inspeccionar, por ejemplo, `raise params.inspect`
