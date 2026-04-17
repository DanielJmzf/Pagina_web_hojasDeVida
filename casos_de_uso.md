# Diagrama de Casos de Uso - MediApp (Actualizado)

A continuación, presento el diagrama de casos de uso estructurado utilizando Mermaid para reflejar exactamente todas las funciones que hemos implementado en la aplicación, de forma idéntica al diagrama original que facilitaste.

```mermaid
flowchart LR
    %% Clases para estilos de los nodos
    classDef actor fill:#f9f9f9,stroke:#333,stroke-width:2px,shape:circle
    classDef useCase fill:#8efc8e,stroke:#333,stroke-width:2px,rx:20,ry:20
    classDef useCaseExt fill:#e0e0e0,stroke:#333,stroke-width:2px,rx:20,ry:20

    %% Actores
    Invitado(("Usuario invitado"))
    User(("Usuario"))
    Admin(("Administrador"))
    
    %% Aplicar clase de actor (ficticio, Mermaid usa subgrafos o nodos circulares)
    class Invitado,User,Admin actor

    %% ==============================
    %% Casos de Uso: Usuario Invitado
    %% ==============================
    Registro([Registrar su cuenta]):::useCase
    VerGeneral([Ver pagina general]):::useCase

    Invitado --- Registro
    Invitado --- VerGeneral

    %% ==============================
    %% Casos de Uso: Usuario
    %% ==============================
    Login([Iniciar sesion]):::useCase
    CerrarSesion([Cerrar sesion]):::useCase
    VerPerfil([Ver su perfil]):::useCase
    
    CambiarPass([Cambiar contraseña]):::useCase
    CambiarFoto([Cambiar Foto]):::useCase
    EliminarCuenta([Eliminar cuenta]):::useCaseExt

    User --- Login
    VerGeneral -. "<< extend >>" .-> Login

    %% Extensiones del Login para usuarios normales
    CerrarSesion -. "<< extend >>" .-> Login
    VerPerfil -. "<< extend >>" .-> Login

    %% Extensiones del Perfil
    CambiarPass -. "<< extend >>" .-> VerPerfil
    CambiarFoto -. "<< extend >>" .-> VerPerfil
    EliminarCuenta -. "<< extend >>" .-> VerPerfil

    %% ==============================
    %% Casos de Uso: Administrador
    %% ==============================
    LoginAdmin([Iniciar sesion como Admin]):::useCaseExt
    ListarUsuarios([Listar usuarios]):::useCaseExt
    
    EliminarUser([Eliminar usuario]):::useCaseExt
    EditarUser([Editar usuario]):::useCaseExt
    AgregarUser([Agregar usuario]):::useCaseExt

    Admin --- LoginAdmin
    
    %% Extensiones del Login de Administrador
    ListarUsuarios -. "<< extend >>" .-> LoginAdmin

    %% Extensiones de la Lista de Usuarios
    EliminarUser -. "<< extend >>" .-> ListarUsuarios
    EditarUser -. "<< extend >>" .-> ListarUsuarios
    AgregarUser -. "<< extend >>" .-> ListarUsuarios
```

### Nota de Diseño
* **Verdes:** Representan los casos de uso principales e interacciones cotidianas.
* **Gris:** Representan funciones destructivas o limitadas que antes "faltaban", correspondientes directamente a los recuadros grises de tu imagen (zonas de peligro en usuario y todo el módulo de panel de Control del Administrador). 

> [!NOTE]
> Todo lo que aprecias en este mapa está actualmente funcional en el código a través de la carpeta `backend/` y `frontend/`.
