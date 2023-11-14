## 変更点
### GROUP BYでASCまたはDESCが使えない
MySQL 8.0.13 では、GROUP BY 句の非推奨の ASC 修飾子または DESC 修飾子は削除されています。 以前に GROUP BY ソートに依存していたクエリーでは、以前の MySQL バージョンとは異なる結果が生成される場合があります。 特定のソート順序を生成するには、ORDER BY 句を指定します。<br> 
https://dev.mysql.com/doc/refman/8.0/ja/upgrading-from-previous-series.html#upgrade-sql-changes

### 外部キー制約のネーミング
MySQL 5.7 では、CONSTRAINT symbol 句なしで InnoDB テーブルの FOREIGN KEY 定義を指定するか、symbol なしで CONSTRAINT キーワードを指定すると、InnoDB で生成された制約名が使用されます。<br> 
この動作は MySQL 8.0 で変更され、InnoDB では生成された名前ではなく FOREIGN KEY index_name 値が使用されます。 制約名はスキーマ (データベース) ごとに一意である必要があるため、スキーマごとに一意ではない外部キーインデックス名が原因でエラーが発生しました。<br> 
このようなエラーを回避するために、MySQL 8.0.16 では新しい制約のネーミング動作が元に戻され、InnoDB では生成された制約名が再度使用されます。<br>
https://dev.mysql.com/doc/refman/8.0/ja/upgrading-from-previous-series.html#upgrade-sql-changes

### 整数データ型の表示幅属性は非推奨
 MySQL 8.0.17 では、整数データ型の表示幅属性は非推奨になりました。将来のバージョンの MySQL ではサポートされなくなる予定です。 <br>
 https://dev.mysql.com/doc/refman/8.0/ja/numeric-type-syntax.html

### FLOAT、DOUBLEおよびDECIMALのUNSIGNED属性は非推奨
MySQL 8.0.17 では、FLOAT、DOUBLE および DECIMAL(およびすべてのシノニム) タイプのカラムに対して UNSIGNED 属性は非推奨であり、将来のバージョンの MySQL でサポートされなくなる予定です。 このようなカラムには、かわりに単純な CHECK 制約の使用を検討してください。<br>
https://dev.mysql.com/doc/refman/8.0/ja/numeric-type-syntax.html

### 数値データ型のZEROFILL属性は非推奨
MySQL 8.0.17 では、整数データ型の表示幅属性と同様に、数値データ型の ZEROFILL 属性は非推奨になりました。 ZEROFILL のサポートおよび整数データ型の表示幅は、将来のバージョンの MySQL で削除される予定です。 これらの属性の効果を生成する別の方法の使用を検討してください。 たとえば、アプリケーションでは、LPAD() 関数を使用して、必要な幅まで数値をゼロ埋めしたり、書式設定された数値を CHAR カラムに格納したりできます。 <br>
https://dev.mysql.com/doc/refman/8.0/ja/numeric-type-syntax.html

## 新機能
### 降順インデックスが使えるようになった
MySQL で降順インデックスがサポートされるようになりました: インデックス定義内の DESC は無視されなくなりましたが、キー値が降順で格納されます。 以前は、インデックスを逆の順序でスキャンできましたが、パフォーマンスが低下していました。 降順インデックスは順にスキャンできるため、より効率的です。 降順インデックスを使用すると、オプティマイザが複数カラムインデックスを使用できるようになります (最も効率的なスキャン順序で一部のカラムに昇順が混在し、他のカラムに降順が混在している場合)。<br>
https://dev.mysql.com/doc/refman/8.0/ja/descending-indexes.html

### ウィンドウ関数が使えるようになった
MySQL では、クエリーの各行について、その行に関連する行を使用して計算を実行するウィンドウ関数がサポートされるようになりました。 これには、RANK()、LAG()、NTILE() などの関数が含まれます。 また、複数の既存の集計関数をウィンドウ関数 (SUM() や AVG() など) として使用できるようになりました。<br>
https://dev.mysql.com/doc/refman/8.0/ja/window-function-optimization.html<br>
https://dev.mysql.com/doc/refman/8.0/ja/example-maximum-column-group-row.html

### 非表示カラムが使えるようになった
MySQL では、MySQL 8.0.23 の時点で非表示カラムがサポートされています。 非表示のカラムは通常、クエリーでは非表示ですが、明示的に参照されている場合はアクセスできます。 MySQL 8.0.23 より前は、すべてのカラムが表示されます。<br>
https://dev.mysql.com/doc/refman/8.0/ja/invisible-columns.html
