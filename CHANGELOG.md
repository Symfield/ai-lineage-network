# CHANGELOG — Graph-Ready v1 → v1.1 (2026-08-10)

## Corrections to v1 (defects found in audit)
1. **Direction reversals** fixed against the relationship dictionary:
   - G_E025 now DeepSeek → High-Flyer (SPUN_OUT_FROM = new lab → origin)
   - G_E027 now Zhipu → Tsinghua, G_E028 now Moonshot → Tsinghua (ACADEMIC_SPINOUT_FROM = lab → university)
   - G_E037 now Google Brain → Alphabet, G_E038 now Meta FAIR → Meta Platforms (SUBSIDIARY_OF = division → parent)
2. **Person rows repaired** (G_N024–G_N030): a missing column had shifted inclusion_class/confidence/source_ids;
   rows realigned to the 16-field header. Country filled as professional base where blank.
3. **G_E029 retargeted**: Llama OPEN_SOURCE_INFLUENCE now Meta FAIR → DeepSeek (concrete recipient),
   evidence downgraded to "reported"; previously pointed at OpenAI with abstract-ecosystem description.

## Additions (August 2026 gap-filling research pass)
- **36 new nodes** (G_N031–G_N066): 16 people (Hinton, Shazeer, Schulman, Suleyman, Kai-Fu Lee, Alexandr Wang,
  Yang Zhilin, Leike, Wang Xiaochuan, Jiang Daxin, Yan Junjie, Tang Jie, Mensch, Lample, Lacroix, Zoph),
  Chinese parents (Alibaba, ByteDance, Baidu, Tencent, SenseTime) + Tongyi Lab and ByteDance Seed,
  capital/compute (Amazon, Google Cloud, SoftBank), acqui-hire targets (Inflection, Character.AI, Scale AI),
  Mistral AI, Sinovation, Sogou, MSRA, DNNresearch, CMU, Meta Superintelligence Labs.
- **79 new edges** (G_E039–G_E117), including 5 new DERIVED founder-lineage edges (Sogou→Baichuan,
  MSRA→StepFun, SenseTime→MiniMax, FAIR→Mistral, DeepMind→Mistral), each carrying primitive edge IDs
  and a derivation rule.
- **40 new sources** (S015–S054) and **10 new uncertainty items** (U011–U020).
- Previously isolated nodes de-isolated: MiniMax, Baichuan, 01.AI, StepFun, NVIDIA. Baidu remains
  deliberately edge-less pending lab-level documentation (U016).

## Vocabulary decisions made during merge (review before freeze)
- Research edge "Tang Jie ADVISED Yang Zhilin" (person→person) violated ADVISED (person→lab);
  converted to ADVISED_BY (Yang → Tang, student→advisor), evidence "reported" (U013).
- Yang Zhilin's CMU advisors (Salakhutdinov, Cohen) folded into the STUDIED_AT edge note rather
  than creating advisor person-nodes.
- Microsoft–Inflection and Google–Character.AI encoded as ACQUIRED with explicit
  "acqui-hire-without-acquisition" caveat notes (U014). Consider minting an ACQUIHIRE type.
- Pre-Alphabet "Google" actions (DNNresearch 2013, Google China 2005–09) mapped to the Alphabet
  node with notes, matching v1's handling.
- Research duplicates of already-corrected v1 edges (Zhipu/Moonshot spinouts, Llama retarget)
  were not double-added.
- Four SUBSIDIARY_OF edges added from parent_node fields (Tongyi→Alibaba, Seed→ByteDance,
  MSL→Meta, MSRA→Microsoft, Google Cloud→Alphabet) per the v1 audit rule that parent
  relationships become edges, not attributes.

## Integrity checks passed
No dangling edge references; all derived edges carry primitives; 66 nodes / 117 edges /
53 sources / 20 uncertainty rows.

## v1.1-dashboard (2026-08-10)
- index.html expanded from single radial network into a five-tab dashboard reading the same data/*.csv: Network (force/radial), Timeline braid (institution lifelines + person career threads, click chips to isolate), Migration heatmap (year x channel edge activity, click cells for sourced claims), Export/Import rankings (weighted TEAM_MIGRATION + FOUNDER_LINEAGE), Capital & Compute concentration (two-column link view; dual-role investor+compute pairs emphasized, Google Cloud grouped under Alphabet via parent_node).
- No data changes.

- Loader made layout-agnostic: tries CSVs at root, then data/, then embedded fallback. Zip now ships flat for one-shot picker upload.
