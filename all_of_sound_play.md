# Sound play の全て

@タイトル: 
@説明文: 
@筆者: lighfu
@筆者ATユーザーリンク: 
@記事作成日: 2022/05/31
@記事更新日: 2024/03/18
@タグ: #block #soundplay

<ul>
    <li><a href="#sound-play-の全て">Sound play の全て</a>
        <ul>
            <li><a href="#options">Options</a></li>
            <li><a href="#引数">引数</a></li>
            <li><a href="#技術メモ">技術メモ</a></li>
        </ul>
    </li>
</ul>

<p>Sound play ブロックを使っていますか？</p>
<p>名前の通り、このブロックは音声を再生するためのブロックです。</p>
<p>通知用に音声を再生したり、音楽プレイヤー的なフローチャートで音声を再生するに使えます。</p>
<h2 id="options">Options</h2>
<h3 id="procced">Procced</h3>
<ul>
    <li><code>immediately</code></li>
    <li><code>When completed</code></li>
</ul>
<h2 id="引数">引数</h2>
<h3 id="sound-uri">Sound URI</h3>
<ul>
    <li>許容型: <code>text</code></li>
    <li>想定される値: <strong>Storage Path</strong>, <strong>Streaming URL</strong></li>
</ul>
<h4 id="storage-path">Storage Path</h4>
<ul>
    <li>端末内のファイルへのパス (<code>/storage/emulated/0/</code>… 等)</li>
    <li><code>ContentProviderURI</code> でも可能</li>
</ul>
<p>パスを指定する場合は、Fx を<strong>有効</strong>にしてから、<code>"[絶対パス]"</code> を指定します。</p>
<h4 id="streaming-url">Streaming URL</h4>
<ul>
    <li>音声ファイルがあるURL を指定できます。</li>
    <li>m3u8, m3u はストリーミングできません。</li>
</ul>
<h3 id="audio-stream">Audio stream</h3>

<table>
    <thead>
        <tr>
            <th>ストリーム名</th>
            <th>フラグコード</th>
            <th>説明</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>AudioManager#STREAM_VOICE_CALL</td>
            <td>0 (0x0)</td>
            <td>通話オーディオストリームで再生されます。</td>
        </tr>
        <tr>
            <td>AudioManager#STREAM_SYSTEM</td>
            <td>1 (0x1)</td>
            <td>システムサウンドオーディオストリームで再生されます。</td>
        </tr>
        <tr>
            <td>AudioManager#STREAM_RING</td>
            <td>2 (0x2)</td>
            <td>電話呼び出しオーディオストリームで再生されます。</td>
        </tr>
        <tr>
            <td>AudioManager#STREAM_MUSIC</td>
            <td>3 (0x3)</td>
            <td>音楽オーディオストリームで再生されます。</td>
        </tr>
        <tr>
            <td>AudioManager#STREAM_ALARM</td>
            <td>4 (0x4)</td>
            <td>アラームオーディオストリームで再生されます。</td>
        </tr>
        <tr>
            <td>AudioManager#STREAM_NOTIFICATION</td>
            <td>5 (0x5)</td>
            <td>通知オーディオストリームで再生されます。</td>
        </tr>
    </tbody>
</table>
<h3 id="volume">Volume</h3>
<p>音声ファイルを任意の音量で再生できます。</p>
<ul>
    <li>許容型: <code>number</code>, <code>text (number)</code></li>
    <li>許容範囲: (0-100)</li>
</ul>
<h3 id="start-position">Start position</h3>
<p>ダイアログから指定する場合は分、秒を簡単に指定できますが、Fxを有効にした場合は、秒数で指定します。</p>
<ul>
    <li>許容型: <code>number</code>, <code>text (number)</code></li>
</ul>
<p>分、秒を秒単位に変換するには以下の式で表現できます。</p>
<pre><code>分 * 60 + 秒</code></pre>
<h3 id="repeat">Repeat</h3>
<p>音声ファイルが最後まで再生されたとき、再度最初から再生するかしないかを指定できます。</p>
<ul>
    <li>
        <p>許容型: <code>number</code>, <code>text (number)</code></p>
    </li>
    <li>
        <p>期待値: <code>0</code> もしくは <code>1</code></p>
    </li>
    <li>
        <p>0 = リピートしない</p>
    </li>
    <li>
        <p>1 = リピートする</p>
    </li>
</ul>
<h3 id="audio-focus">Audio focus</h3>

<table>
    <thead>
        <tr>
            <th>タイプ</th>
            <th>説明</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>None</td>
            <td>どちらのリクエストもフォーカスしない</td>
        </tr>
        <tr>
            <td>Normal</td>
            <td>不明な期間をリクエストする</td>
        </tr>
        <tr>
            <td>Transient</td>
            <td>予想される短期間の一時的なリクエスト。</td>
        </tr>
        <tr>
            <td>Transient may duck</td>
            <td>他より少ない音量で継続する可能性がある、予想される短期間の一時的なリクエスト</td>
        </tr>
        <tr>
            <td>Transient exclusive (Android 4.4+)</td>
            <td>Temporary request for an expected short duration where others should be silent.</td>
        </tr>
    </tbody>
</table>
<p>私の環境では Normal しか動作しなかったように感じました。</p>
<p>Noneの説明文をよく見ると、not を nor とタイプミスしているのがわかります。(v1.33.6 確認)</p>
<h3 id="notification-channel">Notification channel</h3>
<p>Sound play 実行時、通知に音声が再生されていることを通知できます。</p>
<p class="center"><img class="screenshot" src="https://gyazo.com/05bb346449659c2bd3a14f45a03240a3/raw" alt="img"></p>
<p>通知を有効にすると簡単な進捗表示(分:秒)と、通知をクリックすることで、音声を停止することが可能です。</p>
<h2 id="技術メモ">技術メモ</h2>
<p>オーディオファイルの再生には、<code>Class android.media.MediaPlayer</code> を使用されています。</p>
<p><code>class/android.media.MediaPlayer</code></p>
