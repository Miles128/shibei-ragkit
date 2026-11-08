# shibei-ragkit

RAG 召回层的公共原语。**零依赖、纯函数、无状态。**

从 [shibei](https://github.com/Miles128/shibei) 与 NoteAI 两个项目中抽出来的重复实现，
只保留「两边语义一致」的部分；存储、索引生命周期、LLM 增强不在本包内。

| 模块 | 内容 |
|---|---|
| `ragkit.fusion` | `rrf_gain` / `rrf_scores`（名次融合）、`weighted_fuse`（分数融合）、`normalize` |
| `ragkit.coverage` | `build_groups` / `coverage_ratio` / `meets_coverage`（查询词覆盖门槛） |
| `ragkit.mmr` | `mmr_select`（有向量用余弦，无向量用词集合 Jaccard） |
| `ragkit.chunking` | `chunk_markdown`（标题层级 + 代码块/表格原子化 + overlap） |
| `ragkit.cache` | `make_cache_key`（稳定 sha1 键） |

## 安装

```bash
pip install "shibei-ragkit @ git+https://github.com/Miles128/shibei-ragkit.git@v0.1.0"
```

或本地开发：

```bash
uv pip install -e .
pytest -q
```

## 设计边界

- ✅ 无状态、纯函数、零第三方依赖
- ✅ 同一份语义被两个以上项目使用
- ❌ 存储引擎（SQLite FTS5 / zvec）
- ❌ 索引生命周期（manifest / 锁 / 重建）
- ❌ LLM 增强（HyDE）与上下文扩展

## License

MIT
