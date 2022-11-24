<script lang="ts">
	import * as api from '../../scripts/api_client.svelte';

	let userId: String = '123';
	let userName: string = 'test';

	//ここはentityのcolumnアノテーションではなくフィールド名と同じにする。
	$: userInfo = { userId: userId, userName: userName };
	function postUser() {
		console.log(userInfo);
		fetch(`${api.BASE_HOST}/user/`, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(userInfo)
		});

		userId = '';
		userName = '';
	}
</script>

<div class="ketsui-form">
	<p>ユーザーを登録します。</p>
	<input type="text" placeholder="ユーザーID" bind:value={userId} name="user-id" />
	<input type="text" placeholder="ユーザー名" bind:value={userName} name="user-name" />
</div>

<div class="action-button">
	<button on:click={() => postUser()} name="do-insert-button">登録</button>
</div>
