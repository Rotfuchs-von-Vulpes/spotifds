<script lang="ts">
	import { goto } from "$app/navigation";
	import { page } from "$app/stores";
	import { db } from "$lib/db";
	import { ipfs } from "$lib/ipfs";
	import type { ISharedPlaylist } from "$lib/types";

	const params = $page.url.searchParams;

	$: title = params.get("title") ?? "unknown";
	$: cid = params.get("cid");

	async function addPlaylist() {
		if (!cid) return;

		let sharedPlaylist: ISharedPlaylist = await (
			await fetch(`https://ipfs.io/api/v0/dag/get?arg=${cid}`)
		).json();

		if (!sharedPlaylist) return;

		let playlistId = await db.playlists.add({
			title
		});

		let songs = (
			await db.songs.bulkAdd(sharedPlaylist.songs, {
				allKeys: true
			})
		).map((id, index) => ({
			...sharedPlaylist.songs[index],
			id
		}));

		let playlistLength = await db.playlistSongs
			.where("playlistId")
			.equals(playlistId as number)
			.count();

		let index = playlistLength - 1;
		await db.playlistSongs.bulkAdd(
			songs.map((song) => ({ playlistId, songId: song.id, index }))
		);

		ipfs?.addAll(
			songs.map((song) => song.cid),
			{
				pin: true
			}
		);
		await ipfs?.pin.add(cid);

		goto("/");
	}
</script>

<h2>Do you want to add this playlist to your library?</h2>
<div class="container">
	<div class="add-playlist-container">
		<h3>
			{title}
		</h3>
		<button class="button" on:click={addPlaylist}>Add Playlist</button>
	</div>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.add-playlist-container {
		display: flex;
		flex-direction: column;

		background-color: var(--secondary-background-color);
		width: 90%;
		padding: 2% 2%;
	}
	div {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
</style>
