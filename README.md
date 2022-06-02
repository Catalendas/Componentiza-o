#  Componentização

![image](https://user-images.githubusercontent.com/82763928/171521043-cca01edc-fbed-4b74-936f-77bb790c44cf.png)

## Sobre o projeto

Esse projeto foi feito apenas para aprendenrmos a fazer a componentização no react que é a habilidade do react de separar as funcionalidades do software em componentes

## Desenvovlimento 

Na parte de desenvolvimento Mudamos o código de lugar.
Foi tudo separado



### SideBar

Nos arquivos abaixo não estão monstrando os imports e as interfaces

``` export function SideBar({handleClickButton, selectedGenreId}: SideProps) {
  
    const [genres, setGenres] = useState<GenreResponseProps[]>([]);

    useEffect( () => {
      api.get<GenreResponseProps[]>('genres').then(response => {
        setGenres(response.data);
      });
    }, []);

    return(
      <nav className="sidebar">
        <span>Watch<p>Me</p></span>

        <div className="buttons-container">
          {genres.map(genre => (
            <Button
              key={String(genre.id)}
              title={genre.title}
              iconName={genre.name}
              onClick={() => handleClickButton(genre.id)}
              selected={selectedGenreId === genre.id}
            />
          ))}
        </div>

    </nav>
    )
  }

```


### Content

``` export function Content({ selectedGenreId, selectedGenre }: ContentProps) {
  
  const [movies, setMovies] = useState<MovieProps[]>([]);

  useEffect(() => {
    api.get<MovieProps[]>(`movies/?Genre_id=${selectedGenreId}`).then(response => {
      setMovies(response.data);
    });
  }, [selectedGenreId]);

  return(

    <div className="container">
        <header>
          <span className="category">Categoria:<span> {selectedGenre.title}</span></span>
        </header>

        <main>
          <div className="movies-list">
            {movies.map(movie => (
              <MovieCard key ={movie.imdbID} title={movie.Title} poster={movie.Poster} runtime={movie.Runtime} rating={movie.Ratings[0].Value} />
            ))}
          </div>
        </main>
      </div>
  )
}
```

### App

```
export function App() {
  const [selectedGenreId, setSelectedGenreId] = useState(1);
   
  const [selectedGenre, setSelectedGenre] = useState<GenreResponseProps>({} as GenreResponseProps);

  function handleClickButton(id: number) {
    setSelectedGenreId(id);
  }

  return (
    <div style={{ display: 'flex', flexDirection: 'row' }}>
      <SideBar selectedGenreId={selectedGenreId} handleClickButton={handleClickButton}/>
      <Content selectedGenre={selectedGenre} selectedGenreId={selectedGenreId}/>
    </div>
  )
}
```


### Tecnologias utilizada

- React Js
- TypeScript
- Webpack
- Babeljs


# Como executar o projeto

- É preciso clonar o Repositório.
- É preciso ter instalado o yarn em sua maquina.
- No terminal dentro da pasta rode o comando yarn e será executado.
- Entre em http://localhost:8080/ elá estará o projeto.


## Front-end

-- Um bom editor de código como o [Vscode](https://code.visualstudio.com/) pode ajudar na hora de visializar a implementação.

