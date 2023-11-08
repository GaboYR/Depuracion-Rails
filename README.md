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
Agregaremos **= @movie.inspect** en cualquier vista (donde el signo = le dice a Haml que ejecute el código e inserta el resultado en la vista) Para este caso, se agregará en **show.html.haml**.
```ruby
-# in app/views/movies/show.html.haml

%h2 Details about #{@movie.title}

%ul#details
  %li
    Rating:
    = @movie.rating
  %li
    Released on:
    = @movie.release_date.strftime("%B %d, %Y")

%h3 Description:
= link_to 'Edit info', edit_movie_path(@movie)
= link_to 'Back to movie list', movies_path

= @movie.inspect
```
Ahora agregamos a la función `show` lo sgte para ver el manejo de excepciones
```ruby
def show
    id = params[:id] # retrieve movie ID from URI route
    @movie = Movie.find(id) # look up movie by unique ID
    # will render render app/views/movies/show.html.haml by default
    raise params.inspect
  end
```

Finalmente corremos el servidor con el depurador, para ello debemos previamente: 
Verificar que la gema byebug este en el gemfile, ejecutamos el servidor con rails server --debugger. 

