<script>
	import style from './style.module.scss';
	import Toggle from "../../components/Toggle/toggle.svelte";
	import Select from '../../components/Select/select.svelte';
	import languageStrings from '../../libs/languages.js';
	let strings = languageStrings[localStorage.language];
	let profileTypes = [
		{value: 1, label: strings.settings.profileType.firstType},
		{value: 2, label: strings.settings.profileType.secondType},
		{value: 0, label: strings.settings.profileType.thirdType}
	];
	
	let profileTypeValue = profileTypes.find(c => c.value == localStorage.profile_type);
	
	let languages = [
		{value: 'en', label: 'English'},
		{value: 'ru', label: 'Русский'},
		{value: 'fr', label: 'Français'},
		{value: 'bm', label: 'Bahasa Melayu'}
	];
	
	let languagesValue = languages.find(c => c.value == localStorage.language);
	let isNotificationsToggled = localStorage.enable_notifications == "true";
	
	function changeLanguage(lang) {
		localStorage.language = lang;
		strings = languageStrings[localStorage.language];
		profileTypes = [
			{value: 1, label: strings.settings.profileType.firstType},
			{value: 2, label: strings.settings.profileType.secondType},
			{value: 0, label: strings.settings.profileType.thirdType}
		];
	}
</script>

<svelte:head>
	<title>Settings</title>
	<meta name="description" content="Settings" />
</svelte:head>

<div class={style.contentBlock}>
	<div class={style.head}>
		<div class={style.title}>
			{strings.settings.title}
		</div>
		<div class={style.description}>
			{strings.settings.launcher}
		</div>
	</div>
	
	<div class={style.allSettingsDiv}>
		<div class={style.settingDiv}>
			<div class={style.settingDescription}>
				<h2>
					{strings.settings.notifications.title}
				</h2>
				<h3>
					{strings.settings.notifications.description}
				</h3>
			</div>
			<Toggle bind:toggled={isNotificationsToggled} on:toggle={(e) => localStorage.enable_notifications = e.detail} />
		</div>
		
		<hr>
		
		<div class={style.settingDiv}>
			<div class={style.settingDescription}>
				<h2>
					{strings.settings.profileType.title}
				</h2>
				<h3>
					{strings.settings.profileType.description}
				</h3>
			</div>
			<Select
				items={profileTypes}
				value={profileTypeValue}
				onChange={(event) => localStorage.profile_type = event.detail.value}
			/>
		</div>
		
		<hr>
		
		<div class={style.settingDiv}>
			<div class={style.settingDescription}>
				<h2>
					{strings.settings.language.title}
				</h2>
				<h3>
					{strings.settings.language.description}
				</h3>
			</div>
			<Select
				items={languages}
				value={languagesValue}
				onChange={(event) => {
					changeLanguage(event.detail.value);
				}}
			/>
		</div>
	</div>
</div>