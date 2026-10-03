# QuestionPunk for Muse Code

Muse Code is separate from the consumer Muse connector. The released Muse Code 1.4.2 build reports “plugins are not available in this build.” Use the direct MCP connection below on that build. The included native skills plugin targets the documented plugin Developer Preview; its presence is not evidence that the released host can install it.

## Released host: direct MCP connection

Merge `settings-merge.json` into `$XDG_CONFIG_HOME/muse/settings.json` (normally `~/.config/muse/settings.json`). Preserve existing settings and servers. The required `schema_version` is `1`; `mcpServers.questionpunk-cloud` uses Streamable HTTP and `https://app.questionpunk.com/api/v1`. Do not add Authorization headers or paste tokens into the file.

```sh
muse mcp login questionpunk-cloud --scope read,write,responses:read
```

Authorize your own QuestionPunk account. Muse discovers OAuth, registers its public client, and stores tokens privately. Start a new session, inspect `/mcp`, and ask: “Use QuestionPunk to create a QA draft with one onboarding feedback question, then read it back. Do not publish it.” Verify the saved draft in QuestionPunk. Keep each user's credentials separate.

## Plugin Developer Preview

On a build that exposes plugin commands:

```sh
muse plugins validate /absolute/path/to/questionpunk
muse plugins install /absolute/path/to/questionpunk
```

The native manifest declares four research skills and no hooks, commands, or embedded MCP servers. Authenticated MCP must use the settings connection above, because plugin MCP definitions cannot use credentials and portable `mcp.json` declarations stay inactive in the documented compatibility adapter. Do not claim a plugin marketplace listing: Meta has not provided a public plugin catalog in these docs.

Sources checked October 3, 2026: [MCP and OAuth](https://meta-models.github.io/muse-code-sdk/next/guides/extend/mcp-servers/), [plugins](https://meta-models.github.io/muse-code-sdk/next/guides/plugins/), [compatibility](https://meta-models.github.io/muse-code-sdk/next/guides/plugins/concepts/compatibility/). Runtime login and tool execution are separate QA requirements.

## Connection for this build

MCP endpoint: https://app.questionpunk.com/api/v1

QuestionPunk: https://app.questionpunk.com
