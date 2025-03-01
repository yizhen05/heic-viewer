<script>
	import heic2any from "heic2any";

	let file;
	let imageUrl = "";
	let convertedBlob = null;
	let isFileSelected = false; // ファイルが選択されたかどうか

	async function handleFile(event) {
		const selectedFile = event.target.files[0];
		if (!selectedFile) return;

		isFileSelected = true; // ファイル選択時にボタンを有効化

		try {
			convertedBlob = await heic2any({
				blob: selectedFile,
				toType: "image/png",
			});

			// 変換結果が Blob 形式なので、URL を生成
			imageUrl = URL.createObjectURL(convertedBlob);
		} catch (error) {
			console.error("HEIC変換エラー:", error);
			convertedBlob = null;
			imageUrl = "";
		}
	}
</script>

<main>
	<input type="file" accept=".heic" on:change={handleFile} />
	<button on:click={() => {}} disabled={!isFileSelected}>表示</button>

	{#if imageUrl}
		<img
			src={imageUrl}
			alt="変換された HEIC ファイル"
			style="max-width: 100%;"
		/>
	{/if}
</main>

<!-- <script>
</script>

<main>
	<input type="file" name="example" accept=".heic" />
</main>

<style>
</style> -->
