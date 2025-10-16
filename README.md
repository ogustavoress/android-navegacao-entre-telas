# Navegação Entre Telas com Jetpack Compose

**Exemplo didático** de navegação entre telas em Android usando **Jetpack Compose** + **Navigation Compose**, com passagem de parâmetros, Scaffold, innerPadding, NavController etc.

---

## Tecnologias

- Kotlin
- Jetpack Compose
- Navigation Compose
- Material Design 3

---

## Funcionalidades

- Tela de **Login**
- Tela de **Menu**
- Tela de **Perfil*, recebe `nome` e `idade` como parâmetros obrigatórios (via **rota**)
- Tela de **Pedidos**, recebe um `cliente` como parâmetro opcional (via **query**)
- Passagem de parâmetros entre telas
- Gerenciamento centralizado do estado de navegação com `NavController` centralizado
- Layout responsivo com `Scaffold` e `innerPadding`

---

## Estrutura do Projeto

```
app/
└── src/
    └── main/
        └── java/
            └── com/ogustavoress/navegacaoentretelas/
                └── MainActivity.kt
                    └── screens/
                        ├──── LoginScreen.kt
                        ├──── MenuScreen.kt
                        ├──── PerfilScreen.kt
                        └──── PedidosScreen.kt
```

---

## Navegação e Passagem de Parâmetros
A navegação é gerenciada pelo NavHost dentro da MainActivity. 
As rotas são definidas de forma declarativa, e a passagem de parâmetros é feita de maneira segura.

### Definição de rotas (NavHost)
Os argumentos de cada rota são declarados explicitamente com `navArgument`,
evitando erros em tempo de execução.

```
NavHost(navController = navController, startDestination = "login") {
    composable("login") {
        LoginScreen(navController, /* outros parâmetros se houver */)
    }
    composable("menu") {
        MenuScreen(navController)
    }
    composable("perfil/{nome}/{idade}") { backStackEntry ->
        val nome = backStackEntry.arguments?.getString("nome") ?: "Usuário"
        val idade = backStackEntry.arguments
            ?.getString("idade")
            ?.toIntOrNull() ?: 0
        PerfilScreen(navController, nome, idade)
    }
    composable("pedidos?cliente={cliente}") { backStackEntry ->
        val cliente = backStackEntry.arguments?.getString("cliente")
        PedidosScreen(navController, cliente)
    }
}
```

### Navegação entre telas
```
navController.navigate("menu")
navController.navigate("perfil/nomeUsuario/27")
navController.navigate("pedidos?cliente=XPTO")
navController.popBackStack() // volta para a tela anterior
```

## Como Executar o Projeto
1. Clone o repositório
```
   git clone https://github.com/ogustavoress/android-navegacao-entre-telas.git
```    
2. Abra no **Android Studio**
- Abra o projeto na IDE **Android Studio** (versão Hedgehog ou mais recente).
- Aguarde o **Gradle** sincronizar todas as dependências do projeto.

3. Execute o aplicativo:
- Selecione um emulador ou conecte um dispositivo físico Android.
- Clique no botão **Run** (▶️) para compilar e instalar o app.