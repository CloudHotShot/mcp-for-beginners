<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "c3f4ea5732d64bf965e8aa2907759709",
  "translation_date": "2025-07-16T23:11:01+00:00",
  "source_file": "02-Security/mcp-security-best-practices-2025.md",
  "language_code": "ja"
}
-->
# MCP セキュリティベストプラクティス - 2025年7月更新

## MCP実装のための包括的なセキュリティベストプラクティス

MCPサーバーを扱う際は、データ、インフラストラクチャ、ユーザーを保護するために以下のセキュリティベストプラクティスを遵守してください。

1. **入力検証**: インジェクション攻撃や混乱代理問題を防ぐために、常に入力を検証しサニタイズしてください。
   - すべてのツールパラメーターに対して厳格な検証を実装する
   - リクエストが期待される形式に準拠しているかスキーマ検証を行う
   - 処理前に潜在的に悪意のある内容をフィルタリングする

2. **アクセス制御**: MCPサーバーに対して適切な認証と認可を、細かい権限設定で実装してください。
   - Microsoft Entra IDなどの確立されたIDプロバイダーとOAuth 2.0を使用する
   - MCPツールに対してロールベースアクセス制御（RBAC）を実装する
   - 既存の確立されたソリューションがある場合はカスタム認証を実装しない

3. **安全な通信**: MCPサーバーとのすべての通信にHTTPS/TLSを使用し、機密データには追加の暗号化を検討してください。
   - 可能な限りTLS 1.3を設定する
   - 重要な接続には証明書ピンニングを実装する
   - 証明書は定期的に更新し、有効性を確認する

4. **レート制限**: 悪用やDoS攻撃を防ぎ、リソース消費を管理するためにレート制限を実装してください。
   - 予想される使用パターンに基づいて適切なリクエスト制限を設定する
   - 過剰なリクエストに対して段階的な対応を実装する
   - 認証状況に応じたユーザー別のレート制限を検討する

5. **ログ記録と監視**: MCPサーバーの不審な活動を監視し、包括的な監査証跡を実装してください。
   - すべての認証試行とツール呼び出しをログに記録する
   - 不審なパターンに対してリアルタイムのアラートを実装する
   - ログは安全に保管し、改ざんされないようにする

6. **安全なストレージ**: 機密データや資格情報は適切な暗号化を施して保護してください。
   - すべてのシークレットに対してキーボルトや安全な資格情報ストアを使用する
   - 機密データにはフィールドレベルの暗号化を実装する
   - 暗号鍵や資格情報は定期的に更新する

7. **トークン管理**: トークンのパススルー脆弱性を防ぐために、すべてのモデル入力と出力を検証・サニタイズしてください。
   - オーディエンスクレームに基づくトークン検証を実装する
   - 明示的に発行されていないトークンは決して受け入れない
   - 適切なトークンの有効期限管理とローテーションを実施する

8. **セッション管理**: セッションハイジャックや固定攻撃を防ぐために安全なセッション管理を実装してください。
   - 安全で非決定論的なセッションIDを使用する
   - セッションをユーザー固有の情報に紐付ける
   - 適切なセッションの有効期限設定とローテーションを行う

9. **ツール実行のサンドボックス化**: ツールの実行は隔離された環境で行い、侵害時の横移動を防止してください。
   - ツール実行にコンテナ隔離を実装する
   - リソース枯渇攻撃を防ぐためにリソース制限を適用する
   - 異なるセキュリティドメインごとに実行コンテキストを分ける

10. **定期的なセキュリティ監査**: MCP実装と依存関係の定期的なセキュリティレビューを実施してください。
    - 定期的なペネトレーションテストをスケジュールする
    - 自動スキャンツールを使用して脆弱性を検出する
    - 既知のセキュリティ問題に対応するため依存関係を最新に保つ

11. **コンテンツ安全フィルタリング**: 入力と出力の両方に対してコンテンツ安全フィルターを実装してください。
    - Azure Content Safetyなどのサービスを使って有害なコンテンツを検出する
    - プロンプトインジェクションを防ぐためのプロンプトシールド技術を実装する
    - 生成されたコンテンツをスキャンし、潜在的な機密データ漏洩を検出する

12. **サプライチェーンセキュリティ**: AIサプライチェーンのすべてのコンポーネントの整合性と真正性を検証してください。
    - 署名付きパッケージを使用し、署名を検証する
    - ソフトウェア部品表（SBOM）分析を実施する
    - 依存関係の悪意ある更新を監視する

13. **ツール定義の保護**: ツールの定義やメタデータを保護し、ツールの汚染を防いでください。
    - ツール定義は使用前に検証する
    - ツールメタデータの予期しない変更を監視する
    - ツール定義の整合性チェックを実装する

14. **動的実行監視**: MCPサーバーとツールの実行時の挙動を監視してください。
    - 異常検知のための行動分析を実装する
    - 予期しない実行パターンに対するアラートを設定する
    - ランタイムアプリケーション自己防御（RASP）技術を活用する

15. **最小権限の原則**: MCPサーバーとツールは必要最小限の権限で動作させてください。
    - 各操作に必要な特定の権限のみを付与する
    - 権限の使用状況を定期的に見直し監査する
    - 管理機能にはジャストインタイムアクセスを実装する

**免責事項**：  
本書類はAI翻訳サービス「[Co-op Translator](https://github.com/Azure/co-op-translator)」を使用して翻訳されました。正確性を期しておりますが、自動翻訳には誤りや不正確な部分が含まれる可能性があります。原文の言語によるオリジナル文書が正式な情報源とみなされるべきです。重要な情報については、専門の人間による翻訳を推奨します。本翻訳の利用により生じた誤解や誤訳について、当方は一切の責任を負いかねます。