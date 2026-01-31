# vscode-mcp-dev-enviroment-2026-01

Exemplo de arquivo mcp.json do Visual Studio Code configurado para testes de desenvolvimento locais, integrando o GitHub Copilot a MCP Servers do NuGet, Docker Hub, GitHub, Microsoft Learn e um gerador de dados fake (imagem renatogroffe/dotnet10-consoleapp-mcp-fakedata).

Referências utilizadas:
- [MCP Server do NuGet](https://www.nuget.org/packages/NuGet.Mcp.Server)
- [MCP Server do Docker Hub](https://hub.docker.com/mcp/server/dockerhub/overview)
- [MCP Server do GitHub](https://github.com/github/github-mcp-server)
- [MCP Server do Microsoft Learn](https://learn.microsoft.com/en-us/training/support/mcp)
- [MCP Server de Geração de Dados Fake](https://github.com/renatogroffe/dotnet10-consoleapp-mcp-fakedata)

Arquivo **mcp.json** com as configurações:

```json
{
	"servers": {
		"nuget": {
			"type": "stdio",
			"command": "dnx",
			"args": [
				"NuGet.Mcp.Server@1.1.29",
				"--yes"
			]
		},
		"docker": {
			"command": "docker",
			"args": [
				"run",
				"-i",
				"--rm",
				"-e",
				"HUB_PAT_TOKEN=${input:hub_pat_token}",
				"mcp/dockerhub"
			],
			"type": "stdio"
		},
        "github": {
            "type": "http",
            "url": "https://api.githubcopilot.com/mcp/"
        },
		"microsoft-learn": {
			"url": "https://learn.microsoft.com/api/mcp",
			"type": "http"
		},
		"dotnet10-consoleapp-fakedata": {
			"command": "docker",
			"args": [
				"run",
				"-i",
				"--rm",
				"renatogroffe/dotnet10-consoleapp-mcp-fakedata:2"
			],
			"type": "stdio"
		}
	},
	"inputs": [
		{
			"id": "hub_pat_token",
			"type": "promptString",
			"description": "Docker Hub Personal Access Token",
			"password": true
		}
	]
}
```
