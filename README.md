using Microsoft.AspNetCore.Http.HttpResults;
using Microsoft.AspNetCore.Mvc;
using System.ComponentModel;
using WebApplication2.Models;

namespace WebApplication2.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class Biblioteca : ControllerBase
    {
        private static List<Livro> livros =
            new List<Livro>

            {
            new Livro
    {
        Id = 1,
        Name = "Dom Casmurro",
        Autor = "Machado de Assis",
        Ano = "1899",
        Quantidade = 2
    },
    new Livro
    {
        Id = 2,
        Name = "Memórias Póstumas de Brás Cubas",
        Autor = "Machado de Assis",
        Ano = "1881",
        Quantidade = 3
    },
    new Livro
    {
        Id = 3,
        Name = "Grande Sertão: Veredas",
        Autor = "João Guimarães Rosa",
        Ano = "1956",
        Quantidade = 4
    },
    new Livro
    {
        Id = 4,
        Name = "O Cortiço",
        Autor = "Aluísio Azevedo",
        Ano = "1890",
        Quantidade = 4
    },
    new Livro
    {
        Id = 5,
        Name = "Iracema",
        Autor = "José de Alencar",
        Ano = "1865",
        Quantidade = 1
    },
    new Livro
    {
        Id = 6,
        Name = "Macunaíma",
        Autor = "Mário de Andrade",
        Ano = "1928",
        Quantidade = 11
    },
    new Livro
    {
        Id = 7,
        Name = "Capitães da Areia",
        Autor = "Jorge Amado",
        Ano = "1937",
        Quantidade = 2
    },
    new Livro
    {
        Id = 8,
        Name = "Vidas Secas",
        Autor = "Graciliano Ramos",
        Ano = "1938",
        Quantidade = 9
    },
    new Livro
    {
        Id = 9,
        Name = "A Moreninha",
        Autor = "Joaquim Manuel de Macedo",
        Ano = "1844",
        Quantidade = 2
    },
    new Livro
    {
        Id = 10,
        Name = "O Tempo e o Vento",
        Autor = "Erico Verissimo",
        Ano = "1949",
        Quantidade = 1
    },
    new Livro
    {
        Id = 11,
        Name = "A Hora da Estrela",
        Autor = "Clarice Lispector",
        Ano = "1977",
        Quantidade = 1
    },
    new Livro
    {
        Id = 12,
        Name = "O Quinze",
        Autor = "Rachel de Queiroz",
        Ano = "1930",
        Quantidade = 1
    },
    new Livro
    {
        Id = 13,
        Name = "Menino do Engenho",
        Autor = "José Lins do Rego",
        Ano = "1932",
        Quantidade = 5
    },
    new Livro
    {
        Id = 14,
        Name = "Sagarana",
        Autor = "João Guimarães Rosa",
        Ano = "1946",
        Quantidade = 3
    },
    new Livro
    {
        Id = 15,
        Name = "Fogo Morto",
        Autor = "José Lins do Rego",
        Ano = "1943",
        Quantidade = 1
    },

    new Livro
    {
        Id = 16,
        Name = "qwd Morto",
        Autor = "José Lins do Rego",
        Ano = "1943",
        Quantidade = 0
    },

        };
        [HttpGet]
        public ActionResult<List<Livro>> VerLivros()
        {
            return Ok(livros);
        }

        [HttpGet("status/{id}")]
        public ActionResult<Livro>
            StatusLivro(int id)
        {
            var pesquisa = livros.Find(x => x.Id == id);
            if (id == 0 || pesquisa is null)
            {
                return NotFound("Este Livro não foi encontrado");
            }
            return Ok(pesquisa);
        }

        [HttpPost("devolve/{id}")]
        public ActionResult<Livro>
            DevolverLivros(int id)
        {
            var pesquisa = livros.Find(x => x.Id == id);

            if (pesquisa is null)
                return NotFound("Livro não existe");
            pesquisa.Quantidade++;
            pesquisa.Alugado = false;
            return Ok(pesquisa);
            
        }

        [HttpPost("aluga/{id}")]
        public ActionResult<List<Livro>>
            AlugarLivros(int id)
        {
            var pesquisa = livros.Find(x => x.Id == id);
            if (pesquisa is null)
            {
                return NotFound("Livro não encontrado");
            }
            if (pesquisa.Quantidade == 0)
            {
                return NotFound("Livro esgotado");
            }
            pesquisa.Quantidade--;
            pesquisa.Alugado = true;
            return Ok(pesquisa);
            
        }

    }
}

# MODELOS


using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
namespace WebApplication2.Models
{
    [Route("api/[controller]")]
    [ApiController]
    public class Livro
    {
        public int Id { get; set; }
        public string Name { get; set; } = string.Empty;
        public string Autor { get; set; } = string.Empty;
        public string Ano { get; set; } = string.Empty;
        public int Quantidade { get; set; }
        public bool Alugado { get; set; }
    }
}
