# Exemplo de criação de repositório Nuget Localmente

Para criar um repositório Nuget primeiro devemos criar um projeto no Visual Studio do Tipo Class Library .Net Core

![image](https://user-images.githubusercontent.com/30643035/114809529-57d2c800-9d78-11eb-9ad5-9856ce273e43.png)

Nesse projeto colocamos nossas regras e funcionalidade que desejamos compartilhar no repositório Nuget, nesse caso usando uma classe qualquer com um método qualquer de exemplo.

## Configurando o Arquivo CsProj para gerar o nosso pacote

Para isso vamos adicionar um PropertyGroup com o PackageId, Version, Authors, Company e GeneratePackageOnBuild para criar o arquivo .nupkg  

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>
  
  <PropertyGroup>
    <PackageId>MyLibraryNuget</PackageId>
    <Version>1.1.1</Version>
    <Authors>Diogo Schimmelpfennig</Authors>
    <Company>DRS</Company>
    <GeneratePackageOnBuild>true</GeneratePackageOnBuild>
  </PropertyGroup>
  
</Project>
```

Após isso nosso pacote já será gerado toda vez que fizermos Build

![image](https://user-images.githubusercontent.com/30643035/114809600-7afd7780-9d78-11eb-919b-8fdf22c3d1b9.png)


## Criando o Repositório Nuget Localmente

Agora vamos fazer download do executavel do nuget no link  

https://www.nuget.org/downloads  

![image](https://user-images.githubusercontent.com/30643035/114809723-b7c96e80-9d78-11eb-91f8-d12d60c3f44b.png)

Vamos criar um local onde vai ficar os nossos pacotes como por exemplo E:\My-Nuget e vamos colocar o nuget.exe, vamos criar mais uma pasta dentro E:\My-Nuget\Repos

Agora basta executar o seguinte comando

```console
.\nuget.exe add E:\My-Nuget\MyLibraryNuget\MyLibraryNuget\bin\Debug\MyLibraryNuget.1.1.1.nupkg -Source E:\My-Nuget\Repos
```

E o resultado da pasta Repos ficará assim 

![image](https://user-images.githubusercontent.com/30643035/114809996-30c8c600-9d79-11eb-9582-acff562be157.png)



## Usando o repositório Nuget em outros projetos

Para usar o repositório vamos configurar o visual studio da seguinte maneira 

![image](https://user-images.githubusercontent.com/30643035/114810107-68d00900-9d79-11eb-91db-92967ae7b958.png)


Agora vamos no projeto em Nuget Package Manager 

![image](https://user-images.githubusercontent.com/30643035/114810217-96b54d80-9d79-11eb-8cea-e19e64a2ec19.png)

E podemos instalar o nosso pacote 

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="MyLibraryNuget" Version="1.1.1" />
  </ItemGroup> 
  
</Project>
```

```csharp
  ...

  [HttpGet("area/{lado}")]
  public double GetArea(int lado)
  {
      return new MyLibraryNuget.Quadrado().CalcularArea(lado);
  }
  
  ...
```



