# Backend

API REST e servidor de arquivos estáticos em Java, usando apenas o JDK (`com.sun.net.httpserver.HttpServer`). Requer **JDK 11+**.

## Camadas

| Pacote | Classes | Papel |
|---|---|---|
| (raiz) | `ApiServer` | Rotas HTTP, leitura/escrita de JSON, sessão por cookie, arquivos do `frontend/` |
| `controller` | `PacienteController` | Intermedia `ApiServer` e os serviços de paciente; ao excluir um paciente, remove as consultas dele |
| `service` | `PacienteService`, `AgendaService`, `AutenticacaoService` | Regras de negócio e **validações** |
| `repository` | `PacienteRepository` | Armazenamento de pacientes em memória |
| `model` | `Paciente`, `Consulta`, `Usuario` | Entidades |
| `util` | `Seguranca` | Hash de senha (PBKDF2) e geração de token |

## Validações no servidor

- **Paciente:** nome, CPF e convênio obrigatórios; nome ≤ 100 e convênio ≤ 60 caracteres; sem caracteres de controle; CPF com dígitos verificadores válidos e único; foto opcional (PNG/JPEG/WebP em data URL, ≤ 200 mil caracteres).
- **Consulta:** paciente existente; médico obrigatório (≤ 80 caracteres); data/hora válida e futura; um médico não pode ter duas consultas no mesmo horário.
- **Login:** usuário e senha obrigatórios (≤ 40 e ≤ 72 caracteres); credenciais inválidas retornam mensagem genérica (`401`).

## Executar

A partir da **raiz** do projeto, veja o [README principal](../README.md#como-executar) ou use `run.bat`.
