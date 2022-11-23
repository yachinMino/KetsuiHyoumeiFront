<script lang="ts">
	import * as api from '../../scripts/api_client.svelte';

	let ketsui: String;
	let user_id: String = '123';
	let userName: string = 'test';

	//ここはentityのcolumnアノテーションではなくフィールド名と同じにする。
	$: ketsuiInfo = { ketsui: ketsui, userId: user_id };
	function postKetsui() {
		console.log(ketsuiInfo);
		fetch(`${api.BASE_HOST}/ketsui/`, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(ketsuiInfo)
		});

		ketsui = '';
		userName = 'test';
	}
</script>

<div class="ketsui-form">
	<p>ようこそ{userName}さん！</p>

	<p>何をしますか？</p>
	<input type="text" placeholder="決意表明内容" bind:value={ketsui} name="ketsui" />
</div>

<div class="action-button">
	<button on:click={() => postKetsui()} name="do-insert-button">登録</button>
</div>
