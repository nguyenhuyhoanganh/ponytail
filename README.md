# ponytail (minimal)

Bản rút gọn của [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail): chỉ giữ rule và skill, bỏ plugin, hook, MCP, subagent, benchmark. Dùng được cho Claude Code, Codex, Gemini CLI, Cline.

## Cài vào dự án

Copy vào thư mục gốc của dự án (giữ nguyên symlink):

```bash
cp -a AGENTS.md CLAUDE.md GEMINI.md .agents .claude /path/to/project/
```

Dự án đã có sẵn `CLAUDE.md` / `GEMINI.md` thì chỉ cần thêm dòng `@AGENTS.md` vào file đó.

## Thành phần

| File | Vai trò | Agent đọc |
|---|---|---|
| `AGENTS.md` | Rule luôn bật (bản gốc duy nhất) | Codex, Cline |
| `CLAUDE.md` | `@AGENTS.md` | Claude Code |
| `GEMINI.md` | `@AGENTS.md` | Gemini CLI |
| `.agents/skills/` | Skill | Codex, Cline, Gemini CLI |
| `.claude/skills` | Symlink tới `.agents/skills` | Claude Code |

Skill:

- `ponytail [lite|full|ultra]`: chế độ đầy đủ, có mức độ.
- `ponytail-review`: review diff, chỉ tìm over-engineering.
- `ponytail-audit`: như review nhưng quét cả repo.
- `ponytail-debt`: gom các comment `ponytail:` thành sổ nợ kỹ thuật.

Gọi skill: Claude Code `/ponytail-review`, Codex `$ponytail-review`; Gemini và Cline tự kích hoạt theo mô tả, hoặc gọi tên skill trong prompt.

Không có hook nên mức `lite/ultra` chỉ giữ trong phiên hiện tại; rule trong `AGENTS.md` (mức full) luôn bật.

Windows: git cần `core.symlinks=true`, nếu không hãy thay `.claude/skills` bằng bản copy của `.agents/skills`.
