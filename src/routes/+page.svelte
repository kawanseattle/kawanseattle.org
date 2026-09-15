<script lang="ts">
	import { onMount } from 'svelte';
	import { base } from '$app/paths';
	import intlTelInput, { type Iti } from 'intl-tel-input/intlTelInputWithUtils';
	import 'intl-tel-input/styles';

	type Language = 'en' | 'id';

	const programMedia = [
		{
			illustration: `${base}/images/support-settle-editorial-v2.png`,
		},
		{
			illustration: `${base}/images/support-explore-editorial-v2.png`,
		},
		{
			illustration: `${base}/images/support-community-editorial-v2.png`,
		},
		{
			illustration: `${base}/images/support-learn-editorial-v2.png`
		}
	];

	const translations = {
		en: {
			meta: { title: 'Kawan | Your journey. Our guidance.', description: 'KAWAN helps international students settle in, build meaningful friendships, and navigate life in Seattle.' },
			nav: { label: 'Primary navigation', home: 'KAWAN home', about: 'About', help: 'How we help', events: 'Events', connect: 'Connect', toggle: 'Toggle navigation', language: 'Choose language' },
			hero: { kicker: 'Welcome to', statement: 'A friend for your journey.', tagline: 'Helping international students settle in, build meaningful friendships, and navigate life in Seattle.', action: 'Let’s Go' },
			about: { eyebrow: 'about us', title: 'It starts with a friend.', lead: 'KAWAN means “friend” in Bahasa Indonesia.', body1: 'Founded by international students, we understand the challenges of moving to a new country, from navigating school and everyday life to building friendships and planning for the future.', body2: "We're here to help students settle into life in the U.S., build lasting friendships, and find a community that walks alongside them.", body3: '', photoAlt: 'KAWAN community members gathering at Evergreen Christmas Lights in 2025' },
			purpose: { eyebrow: 'why we are here', title: 'Our Purpose', visionLabel: 'our vision', visionTitle1: 'Building a generation', visionTitle2: 'that thrives.', visionBody: 'Building a generation of international students who thrive in life relationally, academically, and professionally, and empower those who come after them.', missionLabel: 'our mission', missionTitle: ['Welcoming.', 'Connecting.', 'Supporting.'], missionBody: 'Welcoming and connecting international students to the broader community while providing friendship, support, resources, and career opportunities.' },
			programsHeading: { eyebrow: 'SUPPORT FOR YOUR JOURNEY', title: 'How Kawan helps', body: 'Practical support, genuine friendships, and a community to help you feel at home.' },
			programs: [
				{ title: 'Settle In', description: 'Help students settle into life in Seattle.', details: '', illustrationAlt: 'A hand-drawn airplane, suitcase, and key', activities: ['Airport pickup', 'Housing guidance', 'Bank account setup', 'State ID / driver’s license guidance', 'Everyday essentials'] },
				{ title: 'Explore Seattle', description: 'Discover the city together.', details: '', illustrationAlt: 'A hand-drawn Space Needle, folded map, and location pin', activities: ['Seattle city trips', 'Local landmarks', 'Hiking', 'Seasonal activities', 'Neighborhood exploration'] },
				{ title: 'Find Community', description: 'Build genuine friendships through simple, relaxed moments together.', details: '', illustrationAlt: 'Hand-drawn game pieces, popcorn, tickets, and coffee mugs', activities: ['Game nights', 'Movie nights', 'Holiday activities', 'Community dinners', 'Monthly gatherings'] },
				{ title: 'Learn & Grow', description: 'Support throughout school and beyond.', details: '', illustrationAlt: 'A hand-drawn open book, laptop, and graduation cap', activities: ['Study nights', 'Study buddies', 'Tutoring', 'Mentorship', 'College guidance', 'Career preparation'] }
			],
			community: { label: 'KAWAN community', photoAlt: 'KAWAN students and families enjoying a community outing by the water', quote: 'Community begins by showing up for one another.' },
			events: { eyebrow: 'Come as you are', title: 'Events', subheading: '', intro: 'Join us throughout the year for opportunities to learn, explore, and build meaningful friendships.', upcoming: 'Upcoming events', calendar: 'event calendar', showEvent: 'Show event on', eventTitle: 'Sunrise Hike', description: 'Start the morning with KAWAN as we hike together, watch the sunrise, and enjoy a beautiful view with new and familiar friends.', photoAlt: 'Three KAWAN friends watching the sunrise from a mountain trail', action: 'RSVP / Learn More' },
			weekdays: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
			moments: { eyebrow: 'Life with KAWAN', title: 'Moments Together', intro: 'A glimpse of the adventures, celebrations, and everyday moments that bring our community closer.', previous: 'Previous hiking photo', next: 'Next hiking photo', choose: 'Choose a hiking photo', show: 'Show hiking photo', hiking: 'Hiking Trips', summerOutings: 'Summer outings', getaways: 'Holiday Getaways', communityGetaway: 'Community getaway', adventures: 'Seattle Adventures', exploring: 'Exploring together', camping: 'Summer Camping', outdoors: 'Outdoor adventures', hikingAlts: ['KAWAN friends gathered along a mountain hiking trail', 'KAWAN community gathered together at a forest waterfall', 'KAWAN friends and families visiting Multnomah Falls'], getawayAlt: 'KAWAN community members together on a holiday trip', seattleAlt: 'Seattle skyline viewed from the water during a KAWAN adventure', campingAlt: 'A glowing campfire during a KAWAN summer camping trip' },
			cta: { eyebrow: 'Get connected', title: 'There’s a place for you here.', body: 'Ready to begin your journey? Meet people who understand and find a community that will walk alongside you.', body2: '', action: 'Get Connected' },
			footer: { tagline: 'A friend for your journey.', links: 'LINKS', involved: 'GET INVOLVED', contact: 'Contact us', copyright: '© 2026 KAWAN Seattle.' },
			form: { close: 'Close', closeLabel: 'Close connection form', thanks: 'Thank you', successTitle: 'We’re glad you’re here.', successBody: 'Your information has been entered.', done: 'Done', eyebrow: 'Get connected', title: 'Let’s get to know you.', intro: 'Share your information and take the first step toward the KAWAN community.', name: 'Name', namePlaceholder: 'Your name', phone: 'Phone number', phoneHint: 'Choose your country, then enter your phone number.', direct: 'Contact KAWAN directly', whatsapp: 'Chat with KAWAN on WhatsApp at +1 206 992 4418', email: 'Email KAWAN at kawanseattle@gmail.com', privacy: 'Your information will be securely forwarded to KAWAN by our form delivery provider.', invalidPhone: 'Please enter a valid phone number for the selected country.', error: 'We could not send your information. Please try again.', sending: 'Sending…', submit: 'Submit' }
		},
		id: {
			meta: { title: 'Kawan | Teman dalam perjalananmu.', description: 'KAWAN membantu pelajar internasional beradaptasi, membangun persahabatan yang bermakna, dan menjalani kehidupan di Seattle.' },
			nav: { label: 'Navigasi utama', home: 'Beranda KAWAN', about: 'Tentang kami', help: 'Dukungan kami', events: 'Acara', connect: 'Terhubung', toggle: 'Buka atau tutup navigasi', language: 'Pilih bahasa' },
			hero: { kicker: 'Selamat datang di', statement: 'Teman dalam perjalananmu.', tagline: 'Kami hadir untuk membantu pelajar internasional beradaptasi dengan kehidupan di Seattle, menemukan teman, dan punya komunitas yang bisa jadi tempat pulang selama jauh dari rumah.', action: 'Mulai Bersama' },
			about: { eyebrow: 'Tentang Kami', title: 'Semua berawal dari seorang teman.', lead: 'KAWAN berarti “teman” dalam bahasa Indonesia.', body1: 'Kami juga pernah menjadi pelajar internasional. Kami tahu rasanya pindah ke negara baru—bingung mengurus hal-hal sehari-hari, beradaptasi dengan kuliah dan budaya baru, mencari teman, sampai memikirkan langkah setelah lulus.', body2: 'Karena itu, KAWAN hadir supaya kamu nggak perlu menjalani semuanya sendirian.', body3: 'Kami ingin menjadi teman yang bisa kamu andalkan selama membangun kehidupan di Seattle—baik saat kamu baru tiba, sedang menjalani kuliah, maupun mulai mempersiapkan masa depan.', photoAlt: 'Komunitas KAWAN berkumpul di Evergreen Christmas Lights pada tahun 2025' },
			purpose: { eyebrow: 'Kenapa KAWAN Ada', title: 'Tujuan Kami', visionLabel: 'Visi Kami', visionTitle1: 'Bertumbuh bersama,', visionTitle2: 'lalu membantu yang berikutnya.', visionBody: 'Kami ingin melihat pelajar internasional bukan hanya berhasil melewati masa kuliah, tapi juga bertumbuh dalam relasi, pendidikan, dan karier—lalu suatu hari bisa membantu mereka yang datang setelahnya.', missionLabel: 'Misi Kami', missionTitle: ['Menyambut.', 'Menghubungkan.', 'Mendampingi.'], missionBody: 'Kami menyambut pelajar internasional, membantu mereka menemukan komunitas, dan mendampingi mereka lewat persahabatan, dukungan praktis, berbagai sumber daya, serta kesempatan untuk belajar dan berkembang.' },
			programsHeading: { eyebrow: '', title: 'Ada KAWAN di Setiap Langkah', body: 'Mulai dari hari pertama di Seattle sampai langkah setelah lulus, ada banyak hal yang lebih mudah kalau dijalani bersama.' },
			programs: [
				{ title: 'Beradaptasi', description: 'Biar hari-hari pertama di Seattle terasa lebih mudah.', details: 'Kami bisa membantu dengan:', illustrationAlt: 'Ilustrasi tangan pesawat, koper, dan kunci', activities: ['Penjemputan dari bandara', 'Mencari tempat tinggal', 'Membuka rekening bank', 'Mengurus State ID / SIM', 'Kebutuhan sehari-hari lainnya'] },
				{ title: 'Jelajahi Seattle', description: 'Kenalan sama kota barumu, bareng-bareng.', details: 'Mulai dari jalan santai sampai hiking dan kegiatan musiman, kami suka menjelajahi Seattle dan sekitarnya bersama.', illustrationAlt: 'Ilustrasi tangan Space Needle, peta lipat, dan penanda lokasi', activities: ['Jalan-jalan di Seattle', 'Mengunjungi tempat-tempat lokal', 'Hiking', 'Kegiatan musiman', 'Menjelajahi berbagai kawasan kota'] },
				{ title: 'Temukan Komunitas', description: 'Karena rumah juga bisa ditemukan lewat orang-orang di sekitar kita.', details: 'Nggak harus selalu acara besar. Kadang persahabatan justru tumbuh dari makan bareng, ngobrol santai, atau sekadar menghabiskan waktu bersama.', illustrationAlt: 'Ilustrasi tangan bidak permainan, popcorn, tiket, dan cangkir kopi', activities: ['Malam permainan', 'Nonton bareng', 'Perayaan hari raya', 'Makan bersama', 'Pertemuan bulanan'] },
				{ title: 'Belajar & Bertumbuh', description: 'Kami juga ada untuk perjalanan kuliah dan langkahmu setelahnya.', details: '', illustrationAlt: 'Ilustrasi tangan buku terbuka, laptop, dan topi wisuda', activities: ['Belajar bersama', 'Teman belajar', 'Bimbingan belajar', 'Mentoring', 'Panduan seputar kuliah', 'Persiapan karier'] }
			],
			community: { label: 'Komunitas KAWAN', photoAlt: 'Pelajar dan keluarga KAWAN menikmati kebersamaan di tepi air', quote: 'Komunitas tumbuh saat kita hadir untuk satu sama lain.' },
			events: { eyebrow: 'Datang apa adanya. Ada tempat untukmu di sini.', title: 'Acara', subheading: 'Yuk, ketemu!', intro: 'Sepanjang tahun, kami mengadakan berbagai kegiatan untuk belajar, jalan-jalan, mencoba hal baru, dan tentunya menghabiskan waktu bersama.', upcoming: 'Acara Mendatang', calendar: 'kalender acara', showEvent: 'Tampilkan acara pada', eventTitle: 'Pendakian Sunrise', description: 'Yuk, mulai pagi bersama KAWAN! Kita akan hiking bareng, menikmati matahari terbit dan pemandangan indah, sambil menghabiskan waktu bersama teman-teman lama dan baru.', photoAlt: 'Tiga teman KAWAN menikmati matahari terbit dari jalur pegunungan', action: 'RSVP / Info Selengkapnya' },
			weekdays: ['Min', 'Sen', 'Sel', 'Rab', 'Kam', 'Jum', 'Sab'],
			moments: { eyebrow: '', title: 'Momen Bersama KAWAN', intro: 'Sedikit cerita dari berbagai perjalanan, perayaan, dan momen sederhana yang kami jalani bersama.', previous: 'Foto hiking sebelumnya', next: 'Foto hiking berikutnya', choose: 'Pilih foto hiking', show: 'Tampilkan foto hiking', hiking: 'Perjalanan Hiking', summerOutings: 'Kegiatan musim panas', getaways: 'Liburan Bersama', communityGetaway: 'Liburan komunitas', adventures: 'Petualangan di Seattle', exploring: 'Menjelajah bersama', camping: 'Camping Musim Panas', outdoors: 'Petualangan di alam', hikingAlts: ['Teman-teman KAWAN berkumpul di jalur pendakian pegunungan', 'Komunitas KAWAN berkumpul di air terjun dalam hutan', 'Teman dan keluarga KAWAN mengunjungi Multnomah Falls'], getawayAlt: 'Komunitas KAWAN menikmati perjalanan liburan bersama', seattleAlt: 'Pemandangan Seattle dari atas air dalam petualangan bersama KAWAN', campingAlt: 'Api unggun dalam perjalanan camping musim panas KAWAN' },
			cta: { eyebrow: 'Mari Terhubung', title: 'Ada tempat untukmu di sini.', body: 'Baru datang ke Seattle? Sudah lama di sini tapi ingin kenal lebih banyak orang? Atau cuma ingin punya teman untuk ngobrol dan jalan bareng?', body2: 'Apa pun ceritamu, kami senang bisa kenalan.', action: 'Mari Terhubung' },
			footer: { tagline: 'Teman dalam perjalananmu.', links: 'TAUTAN', involved: 'AYO TERLIBAT', contact: 'Hubungi kami', copyright: '© 2026 KAWAN Seattle.' },
			form: { close: 'Tutup', closeLabel: 'Tutup formulir', thanks: 'Terima kasih', successTitle: 'Senang kamu ada di sini.', successBody: 'Informasimu sudah kami terima.', done: 'Selesai', eyebrow: 'Mari terhubung', title: 'Yuk, kenalan lebih dekat.', intro: 'Bagikan informasimu dan ambil langkah pertama untuk bergabung dengan komunitas KAWAN.', name: 'Nama', namePlaceholder: 'Namamu', phone: 'Nomor telepon', phoneHint: 'Pilih negaramu, lalu masukkan nomor telepon.', direct: 'Hubungi KAWAN secara langsung', whatsapp: 'Chat dengan KAWAN melalui WhatsApp di +1 206 992 4418', email: 'Kirim email ke KAWAN di kawanseattle@gmail.com', privacy: 'Informasimu akan diteruskan dengan aman kepada KAWAN melalui penyedia layanan formulir kami.', invalidPhone: 'Masukkan nomor telepon yang valid untuk negara yang dipilih.', error: 'Informasimu belum berhasil dikirim. Silakan coba lagi.', sending: 'Mengirim…', submit: 'Kirim' }
		}
	} as const;

	const today = new Date();
	const calendarYear = today.getFullYear();
	const calendarMonth = 8;
	const calendarDate = new Date(calendarYear, calendarMonth, 1);
	const firstWeekday = new Date(calendarYear, calendarMonth, 1).getDay();
	const daysInMonth = new Date(calendarYear, calendarMonth + 1, 0).getDate();
	const calendarDays: Array<number | null> = [
		...Array.from({ length: firstWeekday }, () => null),
		...Array.from({ length: daysInMonth }, (_, index) => index + 1)
	];
	const eventByDay = new Map([[26, 0]]);
	const hikingPhotos = [
		`${base}/images/kawan-hiking-group-2026.jpg`,
		`${base}/images/kawan-hiking-waterfall-group.jpg`,
		`${base}/images/kawan-hiking-multnomah-falls.jpeg`
	];

	let language: Language = 'en';
	$: t = translations[language];
	$: programs = t.programs.map((program, index) => ({ ...program, ...programMedia[index] }));
	$: monthLabel = new Intl.DateTimeFormat(language === 'id' ? 'id-ID' : 'en-US', { month: 'long', year: 'numeric' }).format(calendarDate);
	$: monthName = new Intl.DateTimeFormat(language === 'id' ? 'id-ID' : 'en-US', { month: 'long' }).format(calendarDate);
	$: events = [{ day: 26, title: t.events.eventTitle, description: t.events.description, image: `${base}/images/sunrise-hike.png` }];
	$: eventDateLabel = language === 'id' ? `Sabtu, ${events[selectedEventIndex].day} ${monthName}` : `Saturday, ${monthName} ${events[selectedEventIndex].day}`;
	let menuOpen = false;
	let selectedEventIndex = 0;
	let email = '';
	let submitted = false;
	let heroElement: HTMLElement;
	let connectFormOpen = false;
	let connectName = '';
	let connectPhone = '';
	let phoneInputInstance: Iti | null = null;
	let connectSubmitted = false;
	let connectSubmitting = false;
	let connectError = '';
	let hikingSlideIndex = 2;

	function setLanguage(nextLanguage: Language) {
		language = nextLanguage;
		if (typeof document !== 'undefined') document.documentElement.lang = nextLanguage;
		if (typeof localStorage !== 'undefined') localStorage.setItem('kawan-language', nextLanguage);
	}

	function subscribe() {
		if (email.trim()) {
			submitted = true;
			email = '';
		}
	}

	function openConnectForm() {
		connectSubmitted = false;
		connectError = '';
		connectFormOpen = true;
	}

	function closeConnectForm() {
		connectFormOpen = false;
	}

	function internationalPhoneInput(input: HTMLInputElement) {
		const instance = intlTelInput(input, {
			initialCountry: 'us',
			countrySearch: true,
			separateDialCode: true,
			formatAsYouType: true,
			strictMode: true
		});
		phoneInputInstance = instance;

		const syncPhone = () => {
			connectPhone = input.value;
			connectError = '';
		};
		input.addEventListener('input', syncPhone);
		input.addEventListener('countrychange', syncPhone);

		return {
			destroy() {
				input.removeEventListener('input', syncPhone);
				input.removeEventListener('countrychange', syncPhone);
				instance.destroy();
				if (phoneInputInstance === instance) phoneInputInstance = null;
			}
		};
	}

	async function submitConnectForm() {
		if (!connectName.trim() || !connectPhone.trim() || connectSubmitting) return;
		await phoneInputInstance?.promise;
		if (!phoneInputInstance?.isValidNumber()) {
			connectError = t.form.invalidPhone;
			return;
		}
		const formattedPhone = phoneInputInstance.getNumber();

		connectSubmitting = true;
		connectError = '';
		try {
			const response = await fetch('https://formsubmit.co/ajax/kawanseattle@gmail.com', {
				method: 'POST',
				headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
				body: JSON.stringify({
					name: connectName.trim(),
					phone: formattedPhone,
					_subject: 'New KAWAN Get Connected submission',
					_template: 'table',
					_honey: ''
				})
			});
			if (!response.ok) throw new Error('Submission failed');
			connectSubmitted = true;
		} catch {
			connectError = t.form.error;
		} finally {
			connectSubmitting = false;
		}
	}

	function handleWindowKeydown(event: KeyboardEvent) {
		if (event.key === 'Escape' && connectFormOpen) closeConnectForm();
	}

	function showPreviousHikingPhoto() {
		hikingSlideIndex = (hikingSlideIndex - 1 + hikingPhotos.length) % hikingPhotos.length;
	}

	function showNextHikingPhoto() {
		hikingSlideIndex = (hikingSlideIndex + 1) % hikingPhotos.length;
	}

	onMount(() => {
		const savedLanguage = localStorage.getItem('kawan-language');
		setLanguage(savedLanguage === 'id' ? 'id' : 'en');
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						entry.target.classList.add('visible');
						observer.unobserve(entry.target);
					}
				}
			},
			{ threshold: 0.12 }
		);

		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));

		const updateHeroFade = () => {
			if (!heroElement) return;
			const progress = Math.min(window.scrollY / Math.max(heroElement.offsetHeight, 1), 1);
			heroElement.style.setProperty('--hero-scroll-fade', String(1 - progress * 0.28));
		};
		window.addEventListener('scroll', updateHeroFade, { passive: true });
		updateHeroFade();

		return () => {
			observer.disconnect();
			window.removeEventListener('scroll', updateHeroFade);
		};
	});
</script>

<svelte:window onkeydown={handleWindowKeydown} />

<svelte:head>
	<title>{t.meta.title}</title>
	<meta name="description" content={t.meta.description} />
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label={t.nav.home}>
		<span class="brand-wordmark"><span>kawan</span><small>seattle</small></span>
	</a>

	<nav class:open={menuOpen} aria-label={t.nav.label}>
		<a href="#about" onclick={() => (menuOpen = false)}>{t.nav.about}</a>
		<a href="#programs" onclick={() => (menuOpen = false)}>{t.nav.help}</a>
		<a href="#events" onclick={() => (menuOpen = false)}>{t.nav.events}</a>
	</nav>

	<div class="header-actions">
		<div class="language-toggle" role="group" aria-label={t.nav.language}>
			<button class:active={language === 'en'} type="button" aria-pressed={language === 'en'} onclick={() => setLanguage('en')}>EN</button>
			<span aria-hidden="true">/</span>
			<button class:active={language === 'id'} type="button" aria-pressed={language === 'id'} onclick={() => setLanguage('id')}>ID</button>
		</div>
		<a class="desktop-cta" href="#connect">{t.nav.connect}</a>
		<button
			class="menu-button"
			class:active={menuOpen}
			aria-label={t.nav.toggle}
			aria-expanded={menuOpen}
			onclick={() => (menuOpen = !menuOpen)}
		>
			<span></span><span></span>
		</button>
	</div>
</header>

<main id="top">
	<section class="hero" bind:this={heroElement}>
		<div class="hero-minimal">
			<div class="hero-illustrations" aria-hidden="true">
				<img class="hero-illustration illustration-space-needle" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-board-game" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-water-taxi" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-hiking" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration hero-illustration-mobile" src={`${base}/images/kawan-hero-seattle-sketches-mobile.png`} alt="" />
			</div>
			<div class="hero-content">
				<p class="hero-kicker">{t.hero.kicker}</p>
				<h1><span class="kawan-script">kawan</span></h1>
				<p class="hero-statement">{t.hero.statement}</p>
				<p class="hero-tagline">{t.hero.tagline}</p>
				<div class="hero-actions">
					<a class="button hero-button" href="#connect">{t.hero.action}</a>
				</div>
			</div>
		</div>
	</section>
	<section class="about section-wrap" id="about">
		<div class="illustration-band reveal" id="our-story">
			<div class="illustration-copy">
				<p class="about-eyebrow">{t.about.eyebrow}</p>
				<h2>{t.about.title}</h2>
				<p class="story-lead"><strong>{t.about.lead}</strong></p>
				<p><strong>{t.about.body1}</strong></p>
				<p><strong>{t.about.body2}</strong></p>
				{#if t.about.body3}<p><strong>{t.about.body3}</strong></p>{/if}
			</div>
			<figure class="about-photo-frame">
				<div class="about-photo-crop"><img src={`${base}/images/kawan-community-christmas-2025.jpeg`} alt={t.about.photoAlt} /></div>
			</figure>
		</div>
		<div class="belief-section">
			<div class="belief-heading reveal">
				<p class="about-eyebrow">{t.purpose.eyebrow}</p>
				<h2>{t.purpose.title}</h2>
			</div>
			<div class="about-grid belief-grid">
			<article class="about-card belief-block reveal" id="our-vision">
				<div class="belief-label"><p class="about-label">{t.purpose.visionLabel}</p></div>
				<div class="belief-copy">
					<h3>{t.purpose.visionTitle1}<br />{t.purpose.visionTitle2}</h3>
					<p class="about-description">{t.purpose.visionBody}</p>
				</div>
			</article>
			<article class="about-card belief-block reveal" id="our-mission" style="--delay: 120ms">
				<div class="belief-label"><p class="about-label">{t.purpose.missionLabel}</p></div>
				<div class="belief-copy">
					<h3>{t.purpose.missionTitle[0]}<br />{t.purpose.missionTitle[1]}<br />{t.purpose.missionTitle[2]}</h3>
					<p class="about-description">{t.purpose.missionBody}</p>
				</div>
			</article>
			</div>
		</div>
	</section>

	<section class="programs section-wrap" id="programs">
		<div class="journey-section-heading reveal">
			{#if t.programsHeading.eyebrow}<p class="about-eyebrow">{t.programsHeading.eyebrow}</p>{/if}
			<h2>{t.programsHeading.title}</h2>
			<p>{t.programsHeading.body}</p>
		</div>
		<div class="program-grid minimal support-journey">
			{#each programs as program, index}
				<article class="program-card support-stop reveal" style={`--delay: ${index * 70}ms`}>
					<div class="card-icon support-visual">
						<img src={program.illustration} alt={program.illustrationAlt} />
					</div>
					<div class="support-copy">
						<h3>{program.title}</h3>
						<p>{program.description}</p>
						{#if program.details}<p class="support-details">{program.details}</p>{/if}
						<ul class="support-activities">{#each program.activities as activity}<li>{activity}</li>{/each}</ul>
					</div>
				</article>
			{/each}
		</div>
	</section>

	<section class="community-photo-break reveal" aria-label={t.community.label}>
		<img src={`${base}/images/kawan-community-outing.jpeg`} alt={t.community.photoAlt} />
		<p>{t.community.quote}</p>
	</section>

	<section class="stories events section-wrap" id="events">
		<div class="events-heading reveal">
			<p class="about-eyebrow">{t.events.eyebrow}</p>
			<h2>{t.events.title}</h2>
			{#if t.events.subheading}<h3>{t.events.subheading}</h3>{/if}
			<p>{t.events.intro}</p>
		</div>

		<div class="events-feature reveal">
			<div class="event-calendar" aria-label={`${monthLabel} ${t.events.calendar}`}>
				<div class="calendar-heading"><p>{t.events.upcoming}</p><h3>{monthLabel}</h3></div>
				<div class="calendar-grid calendar-weekdays">
					{#each t.weekdays as weekday}<span>{weekday}</span>{/each}
				</div>
				<div class="calendar-grid calendar-dates">
					{#each calendarDays as day}
						{#if day && eventByDay.has(day)}
							<button
								class:active={eventByDay.get(day) === selectedEventIndex}
								onclick={() => (selectedEventIndex = eventByDay.get(day) ?? 0)}
								onmouseenter={() => (selectedEventIndex = eventByDay.get(day) ?? 0)}
								aria-label={`${t.events.showEvent} ${language === 'id' ? `${day} ${monthName}` : `${monthName} ${day}`}`}
							>{day}</button>
						{:else}<span class:empty={!day}>{day ?? ''}</span>{/if}
					{/each}
				</div>
			</div>

			<article class="featured-event">
				<div class="featured-event-photo"><img src={events[selectedEventIndex].image} alt={t.events.photoAlt} /></div>
				<div class="featured-event-copy">
					<p class="event-date">{eventDateLabel}</p>
					<h3>{events[selectedEventIndex].title}</h3>
					<p>{events[selectedEventIndex].description}</p>
					<button class="button" type="button" onclick={openConnectForm}>{t.events.action} <span>↗</span></button>
				</div>
			</article>
		</div>

		<div class="moments-heading reveal">
			{#if t.moments.eyebrow}<p class="about-eyebrow">{t.moments.eyebrow}</p>{/if}
			<h3>{t.moments.title}</h3>
			<p>{t.moments.intro}</p>
		</div>
		<div class="moments-gallery">
			<figure class="moment moment-wide reveal">
				<div class="hiking-slide" aria-live="polite">
					{#key hikingSlideIndex}
						<img src={hikingPhotos[hikingSlideIndex]} alt={t.moments.hikingAlts[hikingSlideIndex]} />
					{/key}
				</div>
				<button class="slide-arrow slide-previous" type="button" onclick={showPreviousHikingPhoto} aria-label={t.moments.previous}>‹</button>
				<button class="slide-arrow slide-next" type="button" onclick={showNextHikingPhoto} aria-label={t.moments.next}>›</button>
				<div class="slide-dots" aria-label={t.moments.choose}>
					{#each hikingPhotos as _, index}
						<button class:active={index === hikingSlideIndex} type="button" onclick={() => (hikingSlideIndex = index)} aria-label={`${t.moments.show} ${index + 1}`}></button>
					{/each}
				</div>
				<figcaption><strong>{t.moments.hiking}</strong><span>{t.moments.summerOutings}</span></figcaption>
			</figure>
			<figure class="moment moment-tall reveal" style="--delay: 80ms">
				<img src={`${base}/images/kawan-thanksgiving-retreat-cabin.jpeg`} alt={t.moments.getawayAlt} />
				<figcaption><strong>{t.moments.getaways}</strong><span>{t.moments.communityGetaway}</span></figcaption>
			</figure>
			<figure class="moment moment-small reveal" style="--delay: 140ms">
				<img src={`${base}/images/kawan-seattle-adventures.jpeg`} alt={t.moments.seattleAlt} />
				<figcaption><strong>{t.moments.adventures}</strong><span>{t.moments.exploring}</span></figcaption>
			</figure>
			<figure class="moment moment-small reveal" style="--delay: 200ms">
				<img src={`${base}/images/kawan-summer-camping-fire.jpg`} alt={t.moments.campingAlt} />
				<figcaption><strong>{t.moments.camping}</strong><span>{t.moments.outdoors}</span></figcaption>
			</figure>
		</div>
	</section>

	<section class="cta-minimal" id="connect">
		<div class="section-wrap">
			<div class="cta-content reveal">
				<p class="about-eyebrow">{t.cta.eyebrow}</p>
				<h2>{t.cta.title}</h2>
				<p>{t.cta.body}</p>
				{#if t.cta.body2}<p>{t.cta.body2}</p>{/if}
				<div class="cta-actions"><button class="button large" type="button" onclick={openConnectForm}>{t.cta.action} <span>↗</span></button></div>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="footer-main section-wrap">
		<div class="footer-brand">
			<a class="footer-identity" href="#top" aria-label={t.nav.home}>
				<span class="footer-wordmark"><span>kawan</span><small>seattle</small></span>
			</a>
			<p>{t.footer.tagline}</p>
		</div>
		<div class="footer-links">
			<div><strong>{t.footer.links}</strong><a href="#programs">{t.nav.help}</a><a href="#events">{t.nav.events}</a></div>
			<div><strong>{t.footer.involved}</strong><a href="mailto:hello@kawan.org">{t.footer.contact}</a></div>
		</div>
	</div>
	<div class="footer-bottom section-wrap">
		<span>{t.footer.copyright}</span>
	</div>
</footer>

{#if connectFormOpen}
	<div class="connect-modal-backdrop" role="presentation">
		<div class="connect-modal" role="dialog" aria-modal="true" aria-labelledby="connect-form-title">
			<button class="connect-modal-close" type="button" onclick={closeConnectForm} aria-label={t.form.closeLabel}>{t.form.close}</button>
			{#if connectSubmitted}
				<div class="connect-confirmation">
					<p class="about-eyebrow">{t.form.thanks}</p>
					<h2 id="connect-form-title">{t.form.successTitle}</h2>
					<p>{language === 'id' ? `Terima kasih, ${connectName}. ${t.form.successBody}` : `Thanks, ${connectName}. ${t.form.successBody}`}</p>
					<button class="button" type="button" onclick={closeConnectForm}>{t.form.done}</button>
				</div>
			{:else}
				<div class="connect-form-heading">
					<p class="about-eyebrow">{t.form.eyebrow}</p>
					<h2 id="connect-form-title">{t.form.title}</h2>
					<p>{t.form.intro}</p>
				</div>
				<form class="connect-form" onsubmit={(event) => { event.preventDefault(); submitConnectForm(); }}>
					<label for="connect-name">{t.form.name}</label>
					<input id="connect-name" name="name" type="text" autocomplete="name" bind:value={connectName} required placeholder={t.form.namePlaceholder} />
					<label for="connect-phone">{t.form.phone}</label>
					<div class="phone-field">
						<input id="connect-phone" name="phone" type="tel" autocomplete="tel" use:internationalPhoneInput required aria-describedby="connect-phone-hint" />
					</div>
					<p id="connect-phone-hint" class="phone-hint">{t.form.phoneHint}</p>
					<div class="direct-contacts" aria-label={t.form.direct}>
						<a class="direct-contact whatsapp-contact" href="https://wa.me/12069924418" target="_blank" rel="noreferrer" aria-label={t.form.whatsapp}>
							<svg viewBox="0 0 24 24" aria-hidden="true">
								<path d="M20.5 11.8a8.5 8.5 0 0 1-12.6 7.4L3.5 20.5l1.3-4.3a8.5 8.5 0 1 1 15.7-4.4Z" />
								<path d="M8.2 7.7c.2-.4.4-.4.7-.4h.5c.2 0 .4.1.5.5l.8 1.8c.1.3.1.5-.1.7l-.6.8c-.2.2-.2.4 0 .7.5.9 1.2 1.6 2 2.1.3.2.5.2.7 0l.9-1.1c.2-.2.4-.3.7-.2l1.9.9c.3.2.5.3.5.5 0 .2-.1 1.2-.7 1.8-.5.6-1.3.9-2.1.8-1-.1-2.5-.6-4.2-2.1-1.3-1.2-2.3-2.6-2.7-3.7-.4-1-.4-2.1.1-2.8l.1-.3Z" />
							</svg>
							<strong>+1 (206) 992-4418</strong>
						</a>
						<a class="direct-contact gmail-contact" href="mailto:kawanseattle@gmail.com" aria-label={t.form.email}>
							<svg viewBox="0 0 24 24" aria-hidden="true">
								<path class="gmail-blue" d="M3.5 6.5v11" />
								<path class="gmail-red" d="M3.5 6.5 12 13l8.5-6.5" />
								<path class="gmail-green" d="M20.5 6.5v11" />
								<path class="gmail-gold" d="M3.5 17.5h17" />
							</svg>
							<strong>kawanseattle@gmail.com</strong>
						</a>
					</div>
					<p class="connect-privacy">{t.form.privacy}</p>
					{#if connectError}<p class="connect-error" role="alert">{connectError}</p>{/if}
					<button class="button" type="submit" disabled={connectSubmitting}>{connectSubmitting ? t.form.sending : t.form.submit}</button>
				</form>
			{/if}
		</div>
	</div>
{/if}

<style>
	:global(.reveal) {
		opacity: 0;
		transform: translateY(24px);
		transition: opacity 0.7s ease, transform 0.7s ease;
		transition-delay: var(--delay, 0ms);
	}

	:global(.reveal.visible) {
		opacity: 1;
		transform: translateY(0);
	}

	.site-header {
		position: absolute;
		z-index: 20;
		top: 18px;
		left: 50%;
		display: flex;
		width: min(1280px, calc(100% - 64px));
		height: 88px;
		align-items: center;
		justify-content: space-between;
		padding: 0 18px 0 20px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 999px;
		background: rgba(250, 248, 245, 0.7);
		backdrop-filter: blur(8px);
		box-shadow: 0 14px 40px rgba(91, 74, 66, 0.05);
		transform: translateX(-50%);
	}

	.brand {
		display: inline-flex;
		align-items: center;
		font-family: 'Quicksand', sans-serif;
		font-size: 20px;
		font-weight: 700;
		letter-spacing: -0.8px;
		text-transform: lowercase;
	}

	:global(.brand-mark) {
		display: inline-flex;
		width: 42px;
		height: 42px;
		margin-right: 9px;
		color: var(--forest);
	}

	nav {
		display: flex;
		gap: 50px;
		margin-left: 90px;
	}

	nav a {
		position: relative;
		color: var(--ink);
		font-size: 18px;
		font-weight: 500;
	}

	nav a::after {
		position: absolute;
		right: 0;
		bottom: -7px;
		left: 0;
		height: 2px;
		background: var(--gold);
		content: '';
		transform: scaleX(0);
		transition: transform 0.25s ease;
	}

	nav a:hover::after {
		transform: scaleX(1);
	}

	.button {
		display: inline-flex;
		min-height: 52px;
		align-items: center;
		justify-content: center;
		gap: 13px;
		padding: 0 23px;
		border: 1px solid rgba(61, 61, 61, 0.08);
		border-radius: 13px;
		color: #fff;
		background: #6d5c54;
		box-shadow: 0 8px 20px rgba(109, 92, 84, 0.16);
		font-size: 14px;
		font-weight: 600;
		transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
	}

	.button:hover {
		background: #584943;
		transform: translateY(-1px);
		box-shadow: 0 11px 24px rgba(88, 73, 67, 0.2);
	}

	:global(.button.small) {
		min-height: 42px;
		padding: 0 17px;
	}

	.button.large {
		min-height: 60px;
		padding: 0 32px;
		font-size: 16px;
	}

	:global(.button.gold) {
		color: var(--ink);
		background: var(--gold);
		box-shadow: none;
	}

	:global(.button.gold:hover) {
		background: #ffc979;
	}

	.menu-button {
		display: none;
		width: 44px;
		height: 44px;
		padding: 13px 10px;
		border-radius: 50%;
		background: var(--forest);
	}

	.menu-button span {
		display: block;
		width: 100%;
		height: 2px;
		margin: 5px 0;
		background: white;
		transition: transform 0.2s ease;
	}

	/* Hero Section */
	.hero {
		--hero-scroll-fade: 1;
		position: relative;
		min-height: 100vh;
		overflow: hidden;
		background: radial-gradient(circle at 20% 20%, rgba(232, 196, 119, 0.18), transparent 22%),
			radial-gradient(circle at 80% 10%, rgba(155, 143, 134, 0.13), transparent 24%),
			linear-gradient(135deg, #faf8f5 0%, #ede4db 100%);
	}

	.hero::before,
	.hero::after {
		position: absolute;
		content: '';
		border-radius: 50%;
		pointer-events: none;
	}

	.hero::before {
		right: -80px;
		bottom: -70px;
		width: 320px;
		height: 320px;
		background: rgba(232, 196, 119, 0.12);
	}

	.hero::after {
		left: -60px;
		top: 60px;
		width: 200px;
		height: 200px;
		background: rgba(155, 143, 134, 0.08);
	}

	.hero-minimal {
		display: flex;
		width: min(1280px, calc(100% - 64px));
		height: 100vh;
		min-height: 760px;
		margin: auto;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	.hero-content {
		position: relative;
		z-index: 2;
		text-align: center;
		max-width: 600px;
	}

	h1 {
		max-width: 100%;
		margin: 0 0 22px 0;
		color: var(--ink);
		font-family: 'Cormorant Garamond', serif;
		font-size: clamp(72px, 8vw, 128px);
		font-weight: 600;
		line-height: 1.1;
		letter-spacing: -2px;
		text-transform: lowercase;
	}

	.kawan-script {
		font-family: 'Cormorant Garamond', serif;
		font-size: 1.35em;
		font-weight: 800;
		letter-spacing: -1px;
		color: var(--forest);
	}

	:global(.welcome-to-text) {
		font-size: 0.45em;
		font-weight: 500;
	}

	.hero-tagline {
		max-width: 100%;
		margin: 0 0 40px 0;
		color: var(--muted);
		font-size: 22px;
		line-height: 1.6;
		text-transform: lowercase;
	}

	.hero-actions {
		display: flex;
		justify-content: center;
		gap: 20px;
		margin-top: 30px;
	}

	/* Hero Shape */
	:global(.hero-shape) {
		display: none;
	}

	/* About Section */
	.about {
		position: relative;
		min-height: 100vh;
		padding: 120px 0 110px;
		background: radial-gradient(circle at top left, rgba(232, 196, 119, 0.16), transparent 30%),
			linear-gradient(180deg, #f5eeea 0%, #f7f1eb 100%);
	}

	.about::before {
		position: absolute;
		inset: 80px auto auto 8%;
		width: 280px;
		height: 280px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 50%;
		content: '';
	}

	.about::after {
		position: absolute;
		right: 10%;
		bottom: 12%;
		width: 220px;
		height: 220px;
		border-radius: 50%;
		background: rgba(155, 143, 134, 0.08);
		content: '';
	}

	:global(.about-intro) {
		position: relative;
		z-index: 1;
		max-width: 720px;
		margin: 0 auto 52px;
		text-align: center;
	}

	.about-eyebrow {
		margin: 0;
		color: var(--muted);
		font-size: 12px;
		font-weight: 800;
		letter-spacing: 2px;
		text-transform: uppercase;
	}

	.about-grid {
		position: relative;
		z-index: 1;
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 24px;
		max-width: 1180px;
		margin: 0 auto;
	}

	.about-card {
		display: flex;
		flex-direction: column;
		gap: 18px;
		min-height: 300px;
		padding: 34px 28px 30px;
		border: 1px solid rgba(107, 83, 72, 0.1);
		border-radius: 24px;
		background: rgba(255, 255, 255, 0.28);
		box-shadow: 0 18px 40px rgba(91, 74, 66, 0.03);
		transition: transform 0.25s ease, box-shadow 0.25s ease;
	}

	.about-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 24px 48px rgba(91, 74, 66, 0.06);
	}

	.about-label {
		margin: 0;
		font-size: 11px;
		font-weight: 800;
		letter-spacing: 1.8px;
		text-transform: uppercase;
		color: var(--muted);
	}

	.about-card h3 {
		margin: 0;
		font-size: clamp(24px, 2vw, 32px);
		line-height: 1.15;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -0.7px;
		text-transform: lowercase;
	}

	.about-description {
		margin: 0;
		font-size: 16px;
		line-height: 1.75;
		color: var(--muted);
	}

	@media (max-width: 900px) {
		.about {
			min-height: auto;
		}

		.about-grid {
			grid-template-columns: 1fr;
		}
	}

	/* Programs Section */
	.program-grid.minimal {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 24px;
		margin-top: 60px;
	}

	.program-card {
		padding: 48px 32px;
		border-radius: 18px;
		display: flex;
		flex-direction: column;
		gap: 24px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		box-shadow: 0 18px 36px rgba(91, 74, 66, 0.04);
		transition: transform 0.25s ease, box-shadow 0.25s ease;
	}

	.program-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 22px 44px rgba(91, 74, 66, 0.06);
	}

	.card-icon {
		width: 60px;
		height: 60px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--ink);
	}

	.program-card h3 {
		margin: 0;
		font-size: 28px;
		line-height: 1.2;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -0.6px;
	}

	/* Mentor Section */
	:global(.mentor-section) {
		padding: 120px 0;
		background: #ede4db;
	}

	:global(.mentor-minimal) {
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}

	:global(.mentor-dot) {
		width: 80px;
		height: 80px;
		border: 2px solid var(--forest);
		border-radius: 50%;
		margin: 0 auto 40px;
	}

	:global(.mentor-minimal) h2 {
		font-size: 48px;
		margin: 0 0 16px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -1px;
	}

	:global(.mentor-minimal) p {
		color: var(--muted);
		font-size: 16px;
		margin: 0 0 32px 0;
		line-height: 1.6;
	}

	/* Stories Section */
	.stories {
		padding: 100px 0;
	}

	:global(.story-card) {
		max-width: 720px;
		margin: 0 auto;
		padding: 60px;
		background: linear-gradient(180deg, rgba(245,238,234,0.95), rgba(255,255,255,0.7));
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 24px;
		box-shadow: 0 22px 50px rgba(91, 74, 66, 0.04);
	}

	:global(.quote-mark) {
		font-size: 80px;
		color: var(--gold);
		line-height: 0.6;
		margin-bottom: 20px;
	}

	:global(blockquote) {
		margin: 0 0 40px 0;
		font-size: 24px;
		line-height: 1.6;
		color: var(--ink);
		font-style: italic;
	}

	:global(.student) {
		display: flex;
		align-items: center;
		gap: 16px;
		margin-bottom: 32px;
	}

	:global(.student) img {
		width: 60px;
		height: 60px;
		border-radius: 50%;
	}

	:global(.student) strong {
		display: block;
		color: var(--ink);
	}

	:global(.student) span {
		display: block;
		font-size: 13px;
		color: var(--muted);
	}

	:global(.story-progress) {
		display: flex;
		gap: 8px;
		justify-content: center;
	}

	:global(.story-progress) button {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: rgba(91, 74, 66, 0.2);
		border: none;
		cursor: pointer;
		transition: background 0.3s ease;
	}

	:global(.story-progress) button.active {
		background: var(--ink);
	}

	/* CTA Section */
	.cta-minimal {
		padding: 120px 0;
		background: radial-gradient(circle at top left, rgba(232, 196, 119, 0.18), transparent 30%),
			linear-gradient(135deg, #f0dccb 0%, #e8dfd6 100%);
	}

	.cta-content {
		text-align: center;
	}

	.cta-content h2 {
		font-size: 64px;
		margin: 0 0 40px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -2px;
	}

	/* Footer */
	footer {
		background: var(--cream);
		color: var(--ink);
		padding: 60px 0 20px;
	}

	.footer-main {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 60px;
		margin-bottom: 60px;
	}

	.footer-brand p {
		margin: 12px 0;
		color: var(--muted);
		font-size: 14px;
		line-height: 1.6;
	}

	.footer-links {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 40px;
	}

	.footer-links strong {
		display: block;
		font-size: 11px;
		font-weight: 800;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		margin-bottom: 16px;
		color: var(--muted);
	}

	.footer-links a {
		display: block;
		margin-bottom: 12px;
		color: var(--ink);
		text-decoration: none;
		font-size: 14px;
		transition: opacity 0.2s ease;
	}

	.footer-links a:hover {
		opacity: 0.6;
	}

	.footer-bottom {
		padding-top: 20px;
		border-top: 1px solid rgba(91, 74, 66, 0.1);
		display: flex;
		justify-content: space-between;
		font-size: 12px;
		color: var(--muted);
	}

	/* Utilities */
	.section-wrap {
		width: min(1280px, calc(100% - 64px));
		margin: 0 auto;
	}

	/* Responsive */
	@media (max-width: 768px) {
		.hero-minimal {
			flex-direction: column;
			gap: 40px;
			min-height: auto;
			padding: 60px 0;
		}

		h1 {
			font-size: clamp(48px, 10vw, 72px);
		}

		:global(.hero-shape) {
			display: none;
		}

		:global(.about-content) {
			grid-template-columns: 1fr;
			gap: 60px;
		}

		:global(.about-content) h3 {
			font-size: 24px;
		}

		nav {
			display: none;
		}

		.menu-button {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
		}

		.program-grid.minimal {
			grid-template-columns: 1fr;
		}

		:global(.story-card) {
			padding: 40px;
		}

		:global(.mentor-section) {
			padding: 60px 0;
		}

		.cta-minimal {
			padding: 60px 0;
		}

		.cta-content h2 {
			font-size: 42px;
		}

		.footer-main {
			grid-template-columns: 1fr;
			gap: 40px;
		}

		.footer-links {
			grid-template-columns: 1fr;
		}
	}

	/* Friendly, contemporary type and details */
	:global(body) {
		font-family: 'Inter', sans-serif;
	}

	h1,
	h2,
	h3,
	.kawan-script,
	.program-card h3,
	.cta-content h2 {
		font-family: 'Manrope', sans-serif;
	}

	h1 {
		font-weight: 600;
		letter-spacing: -4px;
	}

	:global(.welcome-to-text) {
		font-weight: 600;
		letter-spacing: -1px;
	}

	.kawan-script {
		position: relative;
		display: inline-block;
		z-index: 0;
		padding: 0 18px 6px;
		color: var(--ink);
		font-weight: 800;
		letter-spacing: -5px;
	}

	.kawan-script::before {
		position: absolute;
		z-index: -1;
		right: 0;
		bottom: 8px;
		left: 0;
		height: 32%;
		border-radius: 18px 8px 16px 10px;
		background: #dce5d7;
		content: '';
		transform: rotate(-1deg);
	}

	.program-card {
		border-radius: 24px;
		background: #fff;
		box-shadow: 0 12px 32px rgba(91, 74, 66, 0.055);
	}

	.program-card:nth-child(2) {
		transform: translateY(16px);
	}

	.program-card:nth-child(2):hover {
		transform: translateY(10px);
	}

	.button {
		border-radius: 13px;
	}

	@media (max-width: 768px) {
		h1 {
			letter-spacing: -2.5px;
		}

		.program-card:nth-child(2),
		.program-card:nth-child(2):hover {
			transform: none;
		}
	}

	.illustration-band {
		position: relative;
		display: grid;
		min-height: 540px;
		grid-template-columns: 0.8fr 1.2fr;
		align-items: center;
		gap: 24px;
		overflow: hidden;
		margin: 45px 0 80px;
		padding: 48px 34px 18px 58px;
		border-radius: 36px;
		background: #f1e9e1;
	}

	.illustration-band::before {
		position: absolute;
		top: -90px;
		right: -65px;
		width: 320px;
		height: 320px;
		border: 1px solid rgba(201, 134, 107, 0.25);
		border-radius: 50%;
		content: '';
	}

	:global(.illustration-band img) {
		position: relative;
		z-index: 1;
		width: 100%;
		filter: drop-shadow(0 18px 22px rgba(109, 92, 84, 0.08));
	}

	:global(.about-photo-frame) {
		position: relative;
		z-index: 1;
		margin: 0;
		padding: 10px 10px 15px;
		background: #fff;
		box-shadow: 0 18px 42px rgba(109, 92, 84, 0.12);
		transform: rotate(1.5deg);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}

	:global(.about-photo-frame):hover {
		box-shadow: 0 22px 50px rgba(109, 92, 84, 0.16);
		transform: rotate(0deg) translateY(-3px);
	}

	:global(.about-photo-crop) {
		position: relative;
		aspect-ratio: 1.52;
		overflow: hidden;
		background: #eee7df;
	}

	:global(.about-photo-crop) img {
		position: absolute;
		top: 50%;
		left: 50%;
		width: 145%;
		max-width: none;
		filter: none;
		transform: translate(-50%, -50%);
	}

	.illustration-copy {
		position: relative;
		z-index: 2;
	}

	.illustration-copy p {
		max-width: 410px;
		margin: 0;
		color: var(--muted);
		font-size: 17px;
		line-height: 1.7;
	}

	:global(.hand-note) {
		display: inline-flex;
		align-items: center;
		gap: 10px;
		padding: 0;
		border: 0;
		border-radius: 0;
		background: transparent;
		color: #6d5c54;
		font-size: 11px;
		font-weight: 700;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		transform: none;
	}

	:global(.hand-note)::before {
		width: 24px;
		height: 1px;
		background: #c9866b;
		content: '';
	}

	.about-grid {
		align-items: start;
	}

	.about-card:nth-child(2) {
		margin-top: 28px;
	}

	.about-card:nth-child(3) {
		margin-top: 56px;
	}

	@media (max-width: 768px) {
		.illustration-band { min-height: 0; grid-template-columns: 1fr; padding: 38px 24px 10px; border-radius: 26px; }
		:global(.about-photo-frame) { margin-top: 20px; }
		.about-card:nth-child(2),.about-card:nth-child(3) { margin-top: 0; }
	}

	/* Quiet editorial header */
	.site-header {
		top: 0;
		width: min(1280px, calc(100% - 64px));
		height: 82px;
		padding: 0;
		border: 0;
		border-bottom: 1px solid rgba(61, 61, 61, 0.1);
		border-radius: 0;
		background: transparent;
		backdrop-filter: none;
		box-shadow: none;
	}

	.brand {
		display: flex;
		align-items: baseline;
		gap: 9px;
		font-family: 'Manrope', sans-serif;
		font-size: 19px;
		font-weight: 800;
		letter-spacing: -0.5px;
	}

	:global(.brand small) {
		color: var(--muted);
		font-family: 'Inter', sans-serif;
		font-size: 8px;
		font-weight: 700;
		letter-spacing: 2px;
	}

	nav {
		gap: 31px;
		margin-left: 0;
	}

	nav a {
		color: #56514e;
		font-size: 13px;
		font-weight: 500;
	}

	nav a::after {
		bottom: -8px;
		height: 1px;
		background: #6d5c54;
	}

	.desktop-cta {
		display: inline-flex;
		align-items: center;
		gap: 8px;
		padding: 9px 0 8px;
		border-bottom: 1px solid #6d5c54;
		color: #4e443f;
		font-size: 13px;
		font-weight: 600;
		transition: color 0.2s ease, gap 0.2s ease;
	}

	.desktop-cta:hover {
		gap: 12px;
		color: #c9866b;
	}

	@media (max-width: 768px) {
		.site-header { width: calc(100% - 36px); height: 72px; }
		.desktop-cta { display: none; }
		.menu-button { width: 36px; height: 36px; padding: 7px 4px; border-radius: 0; background: transparent; }
		.menu-button span { width: 24px; margin: 5px auto; background: #3d3d3d; }
	}

	/* Soft, contemporary refinement */
	.hero {
		background: linear-gradient(180deg, #fbf8f4 0%, #f4eee8 100%);
	}

	.hero::before,
	.hero::after,
	:global(.hero-shape),
	.illustration-band::before {
		display: none;
	}

	.kawan-script {
		color: #6d5c54;
		font-weight: 700;
		letter-spacing: -3px;
	}

	.kawan-script::before {
		height: 24%;
		bottom: 10px;
		border-radius: 3px;
		background: #dfe6da;
		transform: none;
	}

	.about {
		background: #fbf8f4;
	}

	.about::before {
		display: none;
	}

	.illustration-band {
		min-height: 500px;
		margin-top: 34px;
		padding: 52px;
		border: 1px solid rgba(109, 92, 84, 0.08);
		border-radius: 24px;
		background: #f3ede6;
	}

	:global(.about-photo-frame),
	:global(.about-photo-frame):hover {
		padding: 8px 8px 14px;
		border-radius: 18px;
		box-shadow: 0 16px 38px rgba(109, 92, 84, 0.1);
		transform: none;
	}

	:global(.about-photo-crop) {
		border-radius: 12px;
	}

	.about-card:nth-child(2),
	.about-card:nth-child(3),
	.program-card:nth-child(2),
	.program-card:nth-child(2):hover {
		margin-top: 0;
		transform: none;
	}

	.program-card {
		border-color: rgba(109, 92, 84, 0.08);
		box-shadow: 0 10px 28px rgba(109, 92, 84, 0.045);
	}

	.cta-minimal {
		background: #e7ece3;
	}

	@media (max-width: 768px) {
		.illustration-band { padding: 36px 22px 22px; border-radius: 18px; }
	}

	/* Warm display type for the opening statement */
	.hero h1,
	.hero :global(.welcome-to-text),
	.hero .kawan-script {
		font-family: 'Fraunces', serif;
	}

	.hero h1 {
		font-weight: 600;
		letter-spacing: -3px;
	}

	.hero :global(.welcome-to-text) {
		font-weight: 500;
		letter-spacing: -0.5px;
	}

	.hero .kawan-script {
		font-weight: 700;
		letter-spacing: -4px;
	}

	/* About story hierarchy */
	:global(.about-intro) {
		max-width: 760px;
		margin-bottom: 40px;
		text-align: center;
	}

	:global(.about-intro) h2,
	.belief-heading h2 {
		margin: 8px 0 0;
		color: var(--ink);
		font-family: 'Fraunces', serif;
		font-size: clamp(44px, 5vw, 66px);
		font-weight: 600;
		line-height: 1;
		letter-spacing: -2px;
	}

	.illustration-band {
		grid-template-columns: 1fr 1fr;
		gap: 58px;
		padding: 54px;
	}

	.illustration-copy p {
		max-width: 520px;
		margin: 0 0 18px;
		font-size: 15px;
		line-height: 1.75;
	}

	.illustration-copy .story-lead {
		margin-top: 24px;
		color: #4f4945;
		font-size: 17px;
	}

	.story-lead strong {
		color: var(--ink);
		font-weight: 650;
	}

	.belief-heading {
		max-width: 680px;
		margin: 90px auto 42px;
		text-align: center;
	}

	.belief-heading .about-eyebrow {
		margin-bottom: 0;
	}

	.about-grid {
		grid-template-columns: repeat(2, minmax(0, 1fr));
		max-width: 940px;
		margin-right: auto;
		margin-left: auto;
	}

	.about-card {
		min-height: 330px;
		padding: 42px;
		border: 1px solid rgba(109, 92, 84, 0.08);
		border-radius: 20px;
		background: #fff;
		box-shadow: 0 10px 28px rgba(109, 92, 84, 0.045);
	}

	.about-card:first-child {
		background: #eef1eb;
	}

	.about-card h3 {
		font-family: 'Manrope', sans-serif;
		font-size: 30px;
		line-height: 1.15;
		letter-spacing: -1.2px;
	}

	@media (max-width: 768px) {
		:global(.about-intro) { margin-bottom: 30px; }
		.illustration-band { grid-template-columns: 1fr; gap: 30px; }
		.belief-heading { margin-top: 70px; }
		.about-grid { grid-template-columns: 1fr; }
		.about-card { min-height: 0; padding: 32px; }
	}

	.hero-content {
		z-index: 3;
	}

	/* Full-bleed page frame */
	:global(main),
	:global(footer) {
		width: 100%;
	}

	.section-wrap {
		width: 100%;
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
	}

	.site-header {
		left: 0;
		width: 100%;
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
		transform: none;
	}

	.hero,
	.hero-minimal {
		width: 100%;
		min-height: 100svh;
	}

	.hero-minimal {
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
	}

	@media (max-width: 768px) {
		.section-wrap,
		.hero-minimal,
		.site-header {
			width: 100%;
			padding-right: 20px;
			padding-left: 20px;
		}
	}

	/* Refined Seattle editorial drawing */
	:global(.seattle-art) {
		position: absolute;
		z-index: 1;
		bottom: -6px;
		left: 50%;
		width: 100vw;
		height: auto;
		max-width: none;
		opacity: 0.72;
		filter: saturate(0.72) contrast(0.94);
		transform: translateX(-50%);
		pointer-events: none;
	}

	@media (max-width: 768px) {
		:global(.seattle-art) {
			left: 50%;
			width: 165vw;
			max-width: none;
			opacity: 0.64;
		}
	}

	/* Separate vision and mission statements */
	.about.section-wrap {
		padding-right: 32px;
		padding-left: 32px;
	}

	:global(.about-intro),
	.belief-heading {
		width: 100%;
		max-width: none;
	}

	.illustration-band {
		width: 100%;
	}

	.about-grid {
		display: grid;
		width: 100%;
		grid-template-columns: 1fr;
		gap: 0;
		max-width: none;
	}

	.about-card,
	.about-card:first-child {
		display: grid;
		min-height: 0;
		grid-template-columns: 190px 1fr;
		gap: 50px;
		align-items: start;
		padding: 48px 0;
		border: 0;
		border-top: 1px solid rgba(109, 92, 84, 0.18);
		border-radius: 0;
		background: transparent;
		box-shadow: none;
	}

	.about-card:last-child {
		border-bottom: 1px solid rgba(109, 92, 84, 0.18);
	}

	.about-card:hover {
		box-shadow: none;
		transform: none;
	}

	.belief-label {
		display: flex;
		align-items: baseline;
		gap: 14px;
	}

	:global(.belief-label span) {
		color: #c9866b;
		font-family: 'Fraunces', serif;
		font-size: 21px;
	}

	.belief-label .about-label {
		margin: 0;
	}

	.belief-copy h3 {
		max-width: 650px;
		margin: 0 0 16px;
		font-family: 'Fraunces', serif;
		font-size: clamp(34px, 4vw, 48px);
		font-weight: 600;
		line-height: 1.08;
		letter-spacing: -1.5px;
	}

	.belief-copy .about-description {
		max-width: 620px;
		margin: 0;
		font-size: 16px;
		line-height: 1.7;
	}

	@media (max-width: 768px) {
		.about.section-wrap {
			padding-right: 20px;
			padding-left: 20px;
		}

		.about-card,
		.about-card:first-child {
			grid-template-columns: 1fr;
			gap: 24px;
			padding: 38px 0;
		}
	}

	/* One continuous journey */
	:global(main) {
		position: relative;
		isolation: isolate;
		overflow: hidden;
		background:
			radial-gradient(circle at 12% 28%, rgba(201, 134, 107, 0.07), transparent 22%),
			radial-gradient(circle at 88% 67%, rgba(167, 180, 158, 0.1), transparent 24%),
			linear-gradient(180deg, #fbf8f4 0%, #f7f1ea 48%, #f5f3ec 76%, #eef2ea 100%);
	}

	:global(.journey-thread) {
		position: absolute;
		z-index: -1;
		inset: 78vh 0 0;
		pointer-events: none;
	}

	:global(.journey-thread) svg {
		display: block;
		width: 100%;
		height: 100%;
		overflow: visible;
	}

	:global(.journey-thread) path {
		fill: none;
		vector-effect: non-scaling-stroke;
	}

	:global(.journey-wash) {
		stroke: rgba(167, 180, 158, 0.12);
		stroke-width: 34;
		stroke-linecap: round;
	}

	:global(.journey-line) {
		stroke: rgba(160, 127, 105, 0.26);
		stroke-width: 1.5;
		stroke-dasharray: 2 8;
		stroke-linecap: round;
	}

	.about,
	:global(.mentor-section),
	.cta-minimal {
		background: transparent;
	}

	.about,
	.programs,
	:global(.mentor-section),
	.stories,
	.cta-minimal {
		position: relative;
		z-index: 1;
	}

	:global(.journey-prologue) {
		max-width: 620px;
		margin: 22px auto 0;
		color: var(--muted);
		font-family: 'Fraunces', serif;
		font-size: 19px;
		line-height: 1.65;
	}

	:global(.journey-vignette) {
		position: relative;
		z-index: 1;
		margin: 0;
		pointer-events: none;
	}

	:global(.journey-vignette img) {
		width: 100%;
		height: auto;
		filter: saturate(0.72);
	}

	:global(.journey-vignette figcaption) {
		position: absolute;
		bottom: 10%;
		left: 50%;
		padding: 8px 14px;
		border: 1px solid rgba(109, 92, 84, 0.1);
		border-radius: 999px;
		color: #6d625c;
		background: rgba(251, 248, 244, 0.82);
		backdrop-filter: blur(8px);
		font-size: 11px;
		font-weight: 650;
		letter-spacing: 1.1px;
		text-transform: uppercase;
		transform: translateX(-50%);
		white-space: nowrap;
	}

	:global(.journey-vignette figcaption span) {
		margin-right: 8px;
		color: #c9866b;
		font-family: 'Fraunces', serif;
		font-size: 15px;
	}

	:global(.journey-vignette-arrival) {
		width: min(1120px, 88vw);
		margin: -34px auto -150px;
		opacity: 0.75;
	}

	.illustration-band {
		z-index: 2;
		border-color: rgba(109, 92, 84, 0.06);
		background: rgba(243, 237, 230, 0.76);
		backdrop-filter: blur(4px);
	}

	.programs {
		padding-top: 150px;
		padding-bottom: 120px;
	}

	.journey-section-heading {
		max-width: 740px;
		margin: 0 auto 36px;
		text-align: center;
	}

	.journey-section-heading h2 {
		margin: 10px 0 18px;
		color: var(--ink);
		font-family: 'Fraunces', serif;
		font-size: clamp(42px, 5vw, 66px);
		font-weight: 600;
		line-height: 1.06;
		letter-spacing: -2px;
	}

	.journey-section-heading > p:last-child {
		max-width: 580px;
		margin: 0 auto;
		color: var(--muted);
		font-size: 16px;
		line-height: 1.7;
	}

	:global(.journey-vignette-daily) {
		width: min(1040px, 84vw);
		margin: -42px auto -170px;
		opacity: 0.6;
	}

	.program-grid.minimal {
		position: relative;
		z-index: 2;
		margin-top: 90px;
	}

	.program-card {
		border-color: rgba(109, 92, 84, 0.09);
		background: rgba(255, 255, 255, 0.7);
		backdrop-filter: blur(9px);
	}

	:global(.mentor-section) {
		padding: 150px 0;
	}

	:global(.mentor-minimal) {
		padding: 70px 42px;
		border-top: 1px solid rgba(109, 92, 84, 0.14);
		border-bottom: 1px solid rgba(109, 92, 84, 0.14);
	}

	:global(.mentor-dot) {
		display: none;
	}

	:global(.journey-marker) {
		position: relative;
		width: 70px;
		height: 42px;
		margin: 0 auto 24px;
	}

	:global(.journey-marker)::before,
	:global(.journey-marker)::after,
	:global(.journey-marker) span {
		position: absolute;
		border-radius: 50% 50% 48% 52%;
		content: '';
	}

	:global(.journey-marker)::before {
		inset: 3px 8px 5px 5px;
		background: rgba(167, 180, 158, 0.2);
		transform: rotate(-8deg);
	}

	:global(.journey-marker)::after {
		inset: 9px 3px 2px 13px;
		border: 1px solid rgba(201, 134, 107, 0.5);
		transform: rotate(7deg);
	}

	.stories {
		padding-top: 110px;
		padding-bottom: 130px;
	}

	:global(.stories-heading) {
		margin-bottom: 54px;
	}

	:global(.story-card) {
		background: rgba(255, 255, 255, 0.55);
		backdrop-filter: blur(9px);
	}

	.cta-minimal {
		padding: 150px 0 170px;
	}

	.cta-content h2 {
		font-family: 'Fraunces', serif;
		font-size: clamp(52px, 7vw, 88px);
		font-weight: 600;
	}

	@media (max-width: 768px) {
		:global(.journey-thread) {
			top: 72vh;
			opacity: 0.65;
		}

		:global(.journey-wash) {
			stroke-width: 20;
		}

		:global(.journey-vignette-arrival),
		:global(.journey-vignette-daily) {
			width: 150vw;
			margin-left: -35vw;
		}

		:global(.journey-vignette-arrival) {
			margin-top: -10px;
			margin-bottom: -70px;
		}

		:global(.journey-vignette-daily) {
			margin-top: -10px;
			margin-bottom: -80px;
		}

		:global(.journey-vignette figcaption) {
			bottom: 4%;
		}

		.programs,
		:global(.mentor-section),
		.stories,
		.cta-minimal {
			padding-top: 90px;
			padding-bottom: 90px;
		}

		.journey-section-heading h2 {
			font-size: 42px;
		}

		:global(.mentor-minimal) {
			padding: 54px 12px;
		}
	}

	/* Reverted editorial experiment
	:global(body) {
		color: #343a35;
		background: #f4efe5;
		font-family: Georgia, 'Times New Roman', serif;
	}

	:global(body::before) {
		position: fixed;
		z-index: 100;
		inset: 0;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.16'/%3E%3C/svg%3E");
		content: '';
		opacity: 0.035;
		pointer-events: none;
	}

	.site-header {
		top: 0;
		width: min(1380px, calc(100% - 72px));
		height: 92px;
		padding: 0;
		border: 0;
		border-bottom: 1px solid rgba(52, 58, 53, 0.18);
		border-radius: 0;
		background: transparent;
		box-shadow: none;
		backdrop-filter: none;
	}

	.brand { gap: 7px; font-family: Arial, sans-serif; font-size: 15px; letter-spacing: 0.18em; text-transform: uppercase; }
	.brand small { padding-left: 9px; border-left: 1px solid rgba(52,58,53,.35); font-size: 8px; letter-spacing: .22em; }
	nav { gap: 38px; margin-left: auto; margin-right: 42px; }
	nav a { font-family: Arial, sans-serif; font-size: 11px; letter-spacing: .12em; text-transform: uppercase; }
	.desktop-cta { padding-bottom: 4px; border-bottom: 1px solid currentColor; font-family: Arial, sans-serif; font-size: 11px; letter-spacing: .12em; text-transform: uppercase; }

	.hero {
		min-height: 860px;
		background: #f4efe5;
	}
	.hero::before, .hero::after { display: none; }
	.hero-minimal {
		position: relative;
		display: block;
		width: 100%;
		height: min(100vh, 960px);
		min-height: 800px;
	}
	:global(.seattle-art) { position: absolute; z-index: 0; inset: 0; width: 100%; height: 100%; object-fit: cover; object-position: center; opacity: .96; }
	.hero-content { position: absolute; z-index: 2; top: 24%; left: max(36px, calc((100vw - 1280px) / 2)); max-width: 630px; text-align: left; }
	.hero-kicker { margin-bottom: 26px; font-family: Arial, sans-serif; font-size: 10px; font-weight: 700; letter-spacing: .2em; text-transform: uppercase; }
	h1 { margin-bottom: 28px; font-family: Georgia, 'Times New Roman', serif; font-size: clamp(66px, 7.4vw, 112px); font-weight: 400; line-height: .87; letter-spacing: -.055em; text-transform: none; }
	:global(.welcome-to-text) { font-size: 1em; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script { padding: 0; color: #526258; font-family: Georgia, 'Times New Roman', serif; font-size: 1em; font-style: italic; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script::before, .kawan-script::after { display: none; }
	.hero-tagline { max-width: 470px; margin-bottom: 30px; color: #505851; font-family: Arial, sans-serif; font-size: 15px; line-height: 1.75; text-transform: none; }
	.hero-actions { justify-content: flex-start; margin-top: 0; }
	.button, :global(.button.gold) { min-height: 48px; padding: 0 20px; border: 1px solid #3f4d45; border-radius: 0; color: #f8f4eb; background: #3f4d45; box-shadow: 5px 5px 0 rgba(63,77,69,.13); font-family: Arial, sans-serif; font-size: 11px; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; }
	.button:hover, :global(.button.gold):hover { color: #f8f4eb; background: #2f3c35; box-shadow: 7px 7px 0 rgba(63,77,69,.12); }
	.hero-caption { position: absolute; z-index: 2; right: 4%; bottom: 5%; margin: 0; padding-left: 36px; color: #414a44; font-family: Arial, sans-serif; font-size: 10px; letter-spacing: .08em; }
	.hero-caption::before { position: absolute; top: 50%; left: 0; width: 24px; height: 1px; background: currentColor; content: ''; }
	.hero-caption span { margin-right: 10px; font-weight: 700; text-transform: uppercase; }

	.about, .programs, .stories, .cta-minimal, footer { background: #f4efe5; }
	.about, .programs, .stories { padding-top: 145px; padding-bottom: 145px; }
	.about::before, .about::after { display: none; }
	:global(.about-intro), .journey-section-heading { text-align: left; margin-left: 0; }
	:global(.about-intro) h2, .journey-section-heading h2, :global(.mentor-minimal) h2, .cta-content h2 { font-family: Georgia, 'Times New Roman', serif; font-weight: 400; letter-spacing: -.045em; }
	.about-eyebrow { color: #7b6251; font-family: Arial, sans-serif; font-size: 9px; letter-spacing: .22em; }
	:global(.journey-vignette) img, :global(.about-photo-crop) { border-radius: 0; filter: saturate(.72) sepia(.08); }
	:global(.about-photo-frame) { transform: rotate(1.5deg); }
	.about-grid { grid-template-columns: 1fr 1fr; gap: 0; border-top: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); }
	.about-card { min-height: 0; padding: 42px; border: 0; border-radius: 0; background: transparent; box-shadow: none; }
	.about-card + .about-card { border-left: 1px solid rgba(52,58,53,.22); }
	.about-card:hover, .program-card:hover { transform: none; box-shadow: none; }
	.program-grid.minimal { gap: 0; border-top: 1px solid rgba(52,58,53,.22); }
	.program-card { min-height: 310px; padding: 42px 34px; border: 0; border-right: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	.card-icon { width: 34px; height: 34px; opacity: .62; }
	.program-card h3 { margin-top: auto; font-family: Georgia, 'Times New Roman', serif; font-size: 32px; font-weight: 400; }
	:global(.mentor-section) { background: #d9d3c4; }
	:global(.mentor-minimal) { border-color: rgba(52,58,53,.3); }
	:global(.story-card) { border: 0; border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	:global(blockquote) { font-family: Georgia, 'Times New Roman', serif; font-size: clamp(26px, 3vw, 40px); line-height: 1.42; }
	:global(.student) img { filter: grayscale(.35) sepia(.15); }
	.cta-minimal { border-top: 1px solid rgba(52,58,53,.18); }
	footer { border-top: 1px solid rgba(52,58,53,.22); }

	@media (max-width: 768px) {
		.site-header { width: calc(100% - 36px); height: 72px; }
		.desktop-cta { display: none; }
		nav.open { position: absolute; top: 72px; left: 0; display: flex; width: 100%; padding: 28px; flex-direction: column; gap: 24px; background: #f4efe5; border-bottom: 1px solid rgba(52,58,53,.2); }
		.menu-button { border-radius: 0; background: #3f4d45; }
		.hero-minimal { height: 820px; min-height: 820px; }
		:global(.seattle-art) { object-position: 62% center; opacity: .58; }
		.hero-content { top: 20%; right: 24px; left: 24px; }
		h1 { font-size: clamp(56px, 18vw, 82px); }
		.hero-tagline { max-width: 360px; }
		.hero-caption { right: 24px; bottom: 26px; }
		.about, .programs, .stories { padding-top: 90px; padding-bottom: 90px; }
		.about-grid { grid-template-columns: 1fr; }
		.about-card + .about-card { border-top: 1px solid rgba(52,58,53,.22); border-left: 0; }
		.program-card { min-height: 220px; border-left: 1px solid rgba(52,58,53,.22); }
		:global(.story-card) { padding: 20px 0; }
	}
	*/

	/* Cohesive watercolor section system with the cover intentionally unchanged */
	:global(main) {
		background: #fbf8f2;
	}

	.about,
	.programs,
	:global(.mentor-section),
	.stories,
	.cta-minimal {
		position: relative;
		z-index: 1;
		background: transparent;
	}

	.about {
		padding-top: 140px;
		background: #fbf8f2;
	}

	.about::before {
		display: block;
		position: absolute;
		top: 0;
		left: 50%;
		width: min(1180px, calc(100% - 64px));
		height: 1px;
		background: rgba(93, 102, 87, 0.14);
		content: '';
		transform: translateX(-50%);
	}

	:global(.about-intro),
	.belief-heading,
	.journey-section-heading {
		max-width: 720px;
		margin-right: auto;
		margin-left: auto;
		text-align: center;
	}

	.about-eyebrow,
	:global(.hand-note) {
		color: #7d5949;
		font-size: 10px;
		letter-spacing: 2.2px;
	}

	.illustration-band {
		position: relative;
		display: grid;
		min-height: 590px;
		grid-template-columns: minmax(280px, 0.8fr) minmax(420px, 1.2fr);
		gap: 70px;
		align-items: center;
		overflow: visible;
		margin: 68px 0 130px;
		padding: 68px 72px;
		border: 1px solid rgba(93, 102, 87, 0.1);
		border-radius: 2px;
		background: #f2eee4;
		box-shadow: 0 28px 70px rgba(76, 70, 59, 0.055);
	}

	.illustration-band::before {
		display: block;
		position: absolute;
		right: -7%;
		bottom: -20%;
		width: 46%;
		height: 58%;
		border: 0;
		background: rgba(180, 192, 171, 0.14);
		content: '';
		filter: blur(36px);
		transform: rotate(-5deg);
	}

	:global(.about-photo-frame),
	:global(.about-photo-frame):hover {
		z-index: 2;
		margin: 0;
		padding: 9px 9px 22px;
		border-radius: 1px;
		background: #fffdf8;
		box-shadow: 0 24px 54px rgba(72, 62, 52, 0.14);
		transform: rotate(1.2deg);
	}

	:global(.about-photo-crop) { border-radius: 0; }

	:global(.story-watercolor) {
		position: absolute !important;
		z-index: 1 !important;
		right: -9%;
		bottom: -27%;
		width: 54% !important;
		max-width: 680px;
		opacity: 0.72;
		filter: saturate(0.62) drop-shadow(0 14px 20px rgba(79, 72, 60, 0.06)) !important;
		pointer-events: none;
	}

	.belief-heading { margin-top: 40px; }
	.about-grid { max-width: 1080px; }
	.about-card,
	.about-card:first-child {
		position: relative;
		grid-template-columns: 180px 1fr;
		padding: 62px 30px;
	}
	.about-card::after {
		position: absolute;
		right: 4%;
		bottom: 18%;
		width: 92px;
		height: 52px;
		border-radius: 55% 45% 52% 48%;
		background: rgba(177, 189, 166, 0.18);
		content: '';
		filter: blur(10px);
		transform: rotate(-8deg);
	}
	.about-card:last-child::after { background: rgba(190, 133, 105, 0.12); transform: rotate(7deg); }

	.programs {
		overflow: hidden;
		padding-top: 150px;
		padding-bottom: 150px;
		background: #eef1e9;
	}
	.programs::before {
		position: absolute;
		top: -70px;
		left: -5%;
		width: 110%;
		height: 130px;
		border-radius: 50%;
		background: #fbf8f2;
		content: '';
	}
	:global(.section-watercolor) { margin: 0; pointer-events: none; }
	:global(.help-watercolor) {
		width: min(860px, 78vw);
		margin: -10px auto -150px;
		opacity: 0.58;
	}
	.program-grid.minimal { margin-top: 120px; }
	.program-card {
		border: 1px solid rgba(78, 92, 77, 0.1);
		border-radius: 2px;
		background: rgba(255, 253, 248, 0.8);
		box-shadow: 0 16px 42px rgba(62, 70, 60, 0.05);
		backdrop-filter: blur(8px);
	}
	.program-card:nth-child(2), .program-card:nth-child(2):hover { transform: none; }
	.card-icon { color: #697867; opacity: 0.65; }

	:global(.mentor-section) {
		overflow: hidden;
		padding: 150px 0 130px;
		background: #f6f1e7;
	}
	:global(.mentor-minimal) {
		display: grid;
		max-width: 1180px;
		grid-template-columns: 0.75fr 1.25fr;
		gap: 64px;
		align-items: center;
		padding: 60px 0;
		border-color: rgba(109, 92, 84, 0.16);
		text-align: left;
	}
	:global(.mentor-copy) { position: relative; z-index: 2; }
	:global(.mentor-minimal) h2 { margin-top: 10px; font-family: 'Fraunces', serif; font-size: clamp(46px, 5vw, 70px); line-height: 1; }
	:global(.mentor-minimal) p { max-width: 470px; font-size: 16px; line-height: 1.75; }
	:global(.community-watercolor) { margin: -80px -16% -90px -5%; opacity: 0.72; }
	:global(.involve-actions) { display: flex; align-items: center; gap: 28px; }

	.stories { padding-top: 140px; padding-bottom: 140px; background: #fbf8f2; }
	:global(.story-card) { max-width: 820px; border-radius: 2px; background: #fffdf8; box-shadow: 0 24px 60px rgba(76, 70, 59, 0.07); }
	.cta-minimal { background: #e4e9df; }

	@media (max-width: 768px) {
		.about { padding-top: 92px; }
		.illustration-band { min-height: 0; grid-template-columns: 1fr; gap: 36px; margin: 44px 0 105px; padding: 38px 24px 100px; }
		:global(.story-watercolor) { right: -28%; bottom: -15%; width: 100% !important; opacity: .55; }
		.about-card, .about-card:first-child { grid-template-columns: 1fr; padding: 42px 4px; }
		.programs { padding-top: 105px; padding-bottom: 100px; }
		:global(.help-watercolor) { width: 135vw; margin: -10px 0 -70px -28vw; }
		.program-grid.minimal { margin-top: 70px; }
		:global(.mentor-section) { padding: 90px 0; }
		:global(.mentor-minimal) { grid-template-columns: 1fr; gap: 20px; padding: 30px 0; }
		:global(.community-watercolor) { width: 130%; margin: -20px -15% -35px; opacity: .62; }
		:global(.involve-actions) { align-items: flex-start; flex-direction: column; gap: 20px; }
		.stories { padding-top: 90px; padding-bottom: 90px; }
	}

	/* Small landmark accents */
	.illustration-band {
		min-height: 0;
		grid-template-columns: 1fr 1fr;
		gap: clamp(40px, 7vw, 96px);
		margin: 60px 0 120px;
		padding: clamp(44px, 6vw, 76px);
		background: #f4f0e7;
		box-shadow: none;
	}
	.illustration-band::before,
	.about-card::after,
	.programs::before { display: none; }
	.illustration-copy { padding-top: 70px; }
	:global(.about-photo-frame),
	:global(.about-photo-frame):hover { transform: rotate(.8deg); }
	:global(.section-accent) {
		display: block;
		width: 132px;
		height: 132px;
		object-fit: contain;
		opacity: .76;
		filter: saturate(.58);
		pointer-events: none;
	}
	:global(.story-accent) {
		position: absolute;
		top: -54px;
		left: -22px;
		width: 150px;
		height: 150px;
	}
	.belief-copy { position: relative; padding-right: 170px; }
	.belief-copy :global(.section-accent) {
		position: absolute;
		top: 50%;
		right: 4px;
		transform: translateY(-50%);
	}
	.programs {
		padding-top: 135px;
		background: #eef1e9;
	}
	:global(.heading-accent) {
		width: 150px;
		height: 120px;
		margin: 24px auto -18px;
	}
	.program-grid.minimal { margin-top: 64px; }
	.program-card { min-height: 280px; }
	:global(.mentor-minimal) {
		grid-template-columns: .9fr 1.1fr;
		gap: clamp(48px, 7vw, 100px);
	}
	:global(.mentor-copy) { padding-top: 72px; }
	:global(.involve-accent) {
		position: absolute;
		top: -72px;
		left: -18px;
		width: 138px;
		height: 138px;
	}
	:global(.involve-photo) {
		margin: 0;
		padding: 8px 8px 18px;
		background: #fffdf8;
		box-shadow: 0 20px 50px rgba(72,62,52,.12);
		transform: rotate(-.8deg);
	}
	:global(.involve-photo) img {
		width: 100%;
		aspect-ratio: 4 / 3;
		object-fit: cover;
		filter: saturate(.72) contrast(.96);
	}
	.stories :global(.heading-accent) { width: 168px; margin-bottom: -4px; }
	:global(.story-card) { box-shadow: none; border: 1px solid rgba(93,102,87,.11); }

	@media (max-width: 768px) {
		.illustration-band { grid-template-columns: 1fr; gap: 40px; padding: 36px 24px; }
		.illustration-copy { padding-top: 62px; }
		:global(.story-accent) { top: -60px; left: -12px; }
		.belief-copy { padding-right: 112px; }
		.belief-copy :global(.section-accent) { right: -14px; width: 108px; height: 108px; }
		:global(.heading-accent) { width: 126px; height: 104px; }
		:global(.mentor-copy) { padding-top: 66px; }
		:global(.involve-accent) { top: -74px; left: -8px; }
	}

	/* Modern editorial refinement and animated line art */
	:global(.reveal) {
		transform: translateY(28px);
		transition: opacity .8s cubic-bezier(.22, 1, .36, 1), transform .8s cubic-bezier(.22, 1, .36, 1);
	}
	:global(.line-accent) {
		display: block;
		width: 132px;
		height: 132px;
		color: #68766b;
		opacity: .68;
		stroke: currentColor;
		stroke-width: 1.35;
		stroke-linecap: round;
		stroke-linejoin: round;
		pointer-events: none;
	}
	:global(.line-accent) path {
		stroke-dasharray: 520;
		stroke-dashoffset: 520;
		transition: stroke-dashoffset 1.7s cubic-bezier(.22, 1, .36, 1) .15s;
	}
	:global(.line-accent .draw-late) { transition-delay: .48s; }
	:global(.visible) :global(.line-accent) path { stroke-dashoffset: 0; }
	:global(.story-accent) { position: absolute; top: -50px; left: -14px; width: 138px; height: 112px; }
	:global(.belief-copy :global(.line-accent)) { position: absolute; top: 50%; right: 10px; width: 126px; height: 126px; transform: translateY(-50%); }
	:global(.heading-accent) { width: 145px; height: 98px; margin: 28px auto -6px; }
	:global(.involve-accent) { position: absolute; top: -68px; left: -10px; width: 138px; height: 106px; }

	.about { padding-top: 156px; padding-bottom: 150px; }
	.illustration-band {
		padding: clamp(52px, 6vw, 78px);
		border-color: rgba(80, 93, 82, .11);
		background: #f8f5ee;
	}
	:global(.about-photo-frame),
	:global(.about-photo-frame):hover { box-shadow: 0 18px 42px rgba(58, 55, 48, .09); transform: none; }
	.about-card,
	.about-card:first-child { transition: padding .35s ease, background .35s ease; }
	.about-card:hover { padding-right: 38px; padding-left: 38px; background: rgba(238, 241, 233, .55); }

	.programs { padding-top: 145px; padding-bottom: 150px; background: #f0f2ec; }
	.program-grid.minimal {
		display: grid;
		grid-template-columns: repeat(6, minmax(0, 1fr));
		gap: 16px;
		max-width: 1180px;
		margin: 72px auto 0;
	}
	.program-card {
		grid-column: span 2;
		min-height: 390px;
		gap: 18px;
		padding: 34px;
		border: 1px solid rgba(76, 91, 78, .12);
		border-radius: 3px;
		background: rgba(255, 255, 252, .72);
		box-shadow: none;
		backdrop-filter: none;
		transition: transform .35s cubic-bezier(.22,1,.36,1), border-color .35s ease, box-shadow .35s ease;
	}
	.program-card:nth-child(4) { grid-column: 2 / span 2; }
	.program-card:hover {
		transform: translateY(-6px);
		border-color: rgba(76, 91, 78, .24);
		box-shadow: 0 18px 42px rgba(58, 68, 59, .07);
	}
	.card-icon { width: 42px; height: 42px; margin-bottom: 8px; color: #68786b; }
	.program-card h3 { margin-top: 0; font-family: 'Fraunces', serif; font-size: 28px; font-weight: 600; letter-spacing: -.7px; }
	.program-card ul { display: flex; flex-wrap: wrap; gap: 7px; margin: 2px 0 8px; padding: 0; list-style: none; }
	.program-card li { padding: 6px 9px; border: 1px solid rgba(104,120,107,.13); border-radius: 999px; color: #666d65; background: rgba(238,241,233,.55); font-size: 10px; letter-spacing: .02em; }

	:global(.mentor-section) { padding-top: 145px; padding-bottom: 145px; }
	:global(.involve-photo) { box-shadow: 0 18px 46px rgba(58,55,48,.1); transform: none; }
	:global(.story-card) { transition: transform .35s ease, border-color .35s ease; }
	:global(.story-card):hover { transform: translateY(-3px); border-color: rgba(93,102,87,.2); }
	.button, nav a { transition-duration: .3s; }

	@media (max-width: 900px) {
		.program-grid.minimal { grid-template-columns: repeat(2, minmax(0, 1fr)); }
		.program-card, .program-card:nth-child(4) { grid-column: auto; }
		.program-card:last-child { grid-column: 1 / -1; }
	}
	@media (max-width: 620px) {
		.program-grid.minimal { grid-template-columns: 1fr; }
		.program-card, .program-card:last-child { grid-column: auto; min-height: 340px; }
		.belief-copy { padding-right: 94px; }
		:global(.belief-copy :global(.line-accent)) { right: -14px; width: 98px; height: 98px; }
	}
	@media (prefers-reduced-motion: reduce) {
		:global(html) { scroll-behavior: auto; }
		:global(.reveal), :global(.reveal.visible) { opacity: 1; transform: none; transition: none; }
		:global(.line-accent) path { stroke-dashoffset: 0; transition: none; }
		.program-card, :global(.story-card), .button { transition: none; }
	}

	.brand-wordmark {
		display: inline-flex;
		flex-direction: column;
		color: #405047;
		font-family: 'Fraunces', serif;
		line-height: .78;
	}
	.brand-wordmark > span {
		font-size: 38px;
		font-weight: 650;
		letter-spacing: -.065em;
	}
	.brand-wordmark small {
		margin-top: 4px;
		font-family: 'Manrope', sans-serif;
		font-size: 11px;
		font-weight: 500;
		line-height: 1;
		letter-spacing: .2em;
		text-align: center;
	}
	.site-header > .brand {
		align-self: stretch;
		align-items: center;
		line-height: 1;
	}
	@media (max-width: 768px) {
		.brand-wordmark > span { font-size: 33px; }
		.brand-wordmark small { margin-top: 4px; font-size: 10px; }
	}

	/* Reverted community first homepage styles
	.hero {
		min-height: 860px;
		background: #f5efe5;
	}
	.hero::before,
	.hero::after { display: block; }
	.hero::before {
		right: auto;
		bottom: -80px;
		left: -70px;
		width: 280px;
		height: 280px;
		background: rgba(174, 188, 162, .2);
		filter: blur(2px);
	}
	.hero::after {
		top: 18%;
		right: 3%;
		left: auto;
		width: 100px;
		height: 64px;
		border: 1px solid rgba(177, 110, 78, .2);
		background: transparent;
		transform: rotate(-8deg);
	}
	.hero-minimal {
		display: grid;
		height: auto;
		min-height: 860px;
		grid-template-columns: minmax(0, .9fr) minmax(460px, 1.1fr);
		gap: clamp(48px, 7vw, 110px);
		align-items: center;
		padding-top: 128px;
		padding-bottom: 72px;
	}
	.hero-content { max-width: 600px; text-align: left; }
	.hero-kicker {
		margin: 0 0 12px;
		color: #886653;
		font-size: 11px;
		font-weight: 750;
		letter-spacing: .22em;
		text-transform: uppercase;
	}
	.hero h1 { margin: 0; font-size: clamp(78px, 9vw, 132px); line-height: .86; text-transform: none; }
	.hero .kawan-script { padding: 0; color: #3d4d43; font-style: normal; letter-spacing: -.07em; text-transform: uppercase; }
	.hero .kawan-script::before { display: none; }
	.hero-statement {
		margin: 26px 0 14px;
		color: #4e4944;
		font-family: 'Fraunces', serif;
		font-size: clamp(27px, 3vw, 40px);
		font-weight: 500;
		line-height: 1.15;
		letter-spacing: -.03em;
	}
	.hero-tagline { max-width: 520px; margin: 0 0 30px; color: #69645f; font-size: 16px; line-height: 1.75; text-transform: none; }
	.hero-actions { justify-content: flex-start; margin: 0; }
	:global(.hero-photo) {
		position: relative;
		z-index: 2;
		margin: 0;
		padding: 10px 10px 28px;
		border-radius: 22px;
		background: #fffdf9;
		box-shadow: 0 28px 70px rgba(71, 60, 49, .16);
		transform: rotate(1.2deg);
	}
	:global(.hero-photo)::before {
		position: absolute;
		z-index: -1;
		top: -18px;
		right: -18px;
		width: 88px;
		height: 88px;
		border-radius: 50%;
		background: #c98262;
		content: '';
		opacity: .32;
	}
	:global(.hero-photo) img { width: 100%; aspect-ratio: 4 / 3; border-radius: 15px; object-fit: cover; filter: saturate(.82) contrast(.97); }
	:global(.hero-photo figcaption) { padding: 14px 8px 0; color: #746b63; font-family: 'Fraunces', serif; font-size: 14px; font-style: italic; }

	.feature-strip {
		position: relative;
		z-index: 4;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 18px;
		padding-top: 72px;
		padding-bottom: 96px;
		background: #fbf8f2;
	}
	.feature-card {
		position: relative;
		min-height: 290px;
		padding: 36px;
		border-radius: 18px;
		background: #fffdf9;
		box-shadow: 0 14px 36px rgba(69, 65, 56, .07);
		transition: transform .35s cubic-bezier(.22,1,.36,1), box-shadow .35s ease;
	}
	.feature-card:nth-child(2) { background: #edf0e8; }
	.feature-card:nth-child(3) { background: #f4e8df; }
	.feature-card:hover { transform: translateY(-6px); box-shadow: 0 20px 44px rgba(69,65,56,.1); }
	.feature-icon { width: 44px; height: 44px; color: #657467; }
	.feature-icon svg { width: 100%; height: 100%; stroke: currentColor; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
	.feature-number { position: absolute; top: 38px; right: 36px; color: #b06f52; font-family: 'Fraunces', serif; font-size: 14px; }
	.feature-card h2 { margin: 52px 0 14px; font-family: 'Fraunces', serif; font-size: 30px; font-weight: 600; letter-spacing: -.04em; }
	.feature-card > p:last-child { margin: 0; color: #6b6862; font-size: 14px; line-height: 1.7; }

	.community-banner { position: relative; overflow: hidden; width: calc(100% - 64px); max-width: 1380px; height: min(72vw, 720px); margin: 0 auto; border-radius: 24px; }
	.community-banner img { width: 100%; height: 100%; object-fit: cover; filter: saturate(.78) contrast(.96); }
	.community-banner::after { position: absolute; inset: 45% 0 0; background: linear-gradient(transparent, rgba(29,35,31,.72)); content: ''; }
	.community-caption { position: absolute; z-index: 2; right: 7%; bottom: 8%; left: 7%; display: flex; align-items: end; justify-content: space-between; gap: 30px; color: white; }
	.community-caption span { font-size: 11px; font-weight: 750; letter-spacing: .2em; text-transform: uppercase; }
	.community-caption p { max-width: 520px; margin: 0; font-family: 'Fraunces', serif; font-size: clamp(28px, 4vw, 52px); line-height: 1.05; text-align: right; }

	.about { padding-top: 150px; }
	.illustration-band {
		grid-template-columns: 1fr .72fr;
		align-items: end;
		max-width: 1060px;
		margin-right: auto;
		margin-left: auto;
		padding: 0 0 100px;
		border: 0;
		border-bottom: 1px solid rgba(90, 94, 83, .16);
		border-radius: 0;
		background: transparent;
	}
	.illustration-copy { padding-top: 60px; }
	.story-pullquote { margin: 0; padding: 34px; border-radius: 18px; color: #556057; background: #edf0e8; font-family: 'Fraunces', serif; font-size: clamp(24px, 3vw, 38px); font-style: italic; line-height: 1.25; transform: rotate(-1deg); }
	.belief-heading { margin-top: 110px; }
	.about-card, .about-card:first-child { border-color: rgba(90,94,83,.13); }

	.programs { background: #edf0e8; }
	.program-card { border-radius: 16px; background: rgba(255,253,248,.82); }
	.events { padding-top: 145px; padding-bottom: 145px; background: #fbf8f2; }
	.events-heading { display: grid; grid-template-columns: 1.2fr .8fr; gap: 80px; align-items: end; max-width: 1120px; margin: 0 auto 64px; }
	.events-heading h2 { max-width: 680px; margin: 10px 0 0; font-family: 'Fraunces', serif; font-size: clamp(46px, 5vw, 68px); font-weight: 600; line-height: 1.04; letter-spacing: -.045em; }
	.events-heading > p { margin: 0; color: #706b65; font-size: 15px; line-height: 1.75; }
	.event-list { max-width: 1120px; margin: 0 auto; border-top: 1px solid rgba(83,92,82,.16); }
	.event-item { display: grid; grid-template-columns: 50px 1fr 1.2fr auto; gap: 30px; align-items: center; padding: 34px 4px; border-bottom: 1px solid rgba(83,92,82,.16); }
	.event-item > span { color: #b17154; font-family: 'Fraunces', serif; font-size: 14px; }
	.event-item div p { margin: 0 0 4px; color: #8a6654; font-size: 9px; font-weight: 750; letter-spacing: .18em; text-transform: uppercase; }
	.event-item h3 { margin: 0; font-family: 'Fraunces', serif; font-size: 27px; font-weight: 600; }
	.event-item > p { margin: 0; color: #706c66; font-size: 14px; line-height: 1.6; }
	.event-item a { padding-bottom: 5px; border-bottom: 1px solid currentColor; color: #4f5c52; font-size: 12px; font-weight: 650; white-space: nowrap; }
	:global(.mentor-section) { background: #f3e9df; }
	.stories { background: #fbf8f2; }
	.cta-minimal { background: #dfe6dc; }

	@media (max-width: 900px) {
		.hero-minimal { min-height: auto; grid-template-columns: 1fr; gap: 54px; padding-top: 130px; padding-bottom: 80px; }
		:global(.hero-photo) { width: min(620px, 92%); justify-self: center; }
		:global(.hero-photo) img { aspect-ratio: 4 / 3; }
		.feature-strip { grid-template-columns: 1fr; }
		.feature-card { min-height: 245px; }
		.events-heading { grid-template-columns: 1fr; gap: 28px; }
		.event-item { grid-template-columns: 36px 1fr; }
		.event-item > p, .event-item > a { grid-column: 2; }
	}
	@media (max-width: 620px) {
		.hero h1 { font-size: clamp(68px, 23vw, 96px); }
		.hero-statement { font-size: 29px; }
		:global(.hero-photo) { width: 100%; padding: 7px 7px 22px; border-radius: 16px; transform: none; }
		:global(.hero-photo) img { border-radius: 11px; }
		.feature-strip { padding-top: 54px; padding-bottom: 72px; }
		.community-banner { width: calc(100% - 24px); height: 72vh; max-height: 620px; border-radius: 16px; }
		.community-caption { align-items: flex-start; flex-direction: column; }
		.community-caption p { text-align: left; }
		.illustration-band { grid-template-columns: 1fr; padding-bottom: 78px; }
		.story-pullquote { margin-top: 10px; }
		.events { padding-top: 100px; padding-bottom: 100px; }
		.event-item { gap: 16px; padding: 28px 0; }
	}

	Seattle outline hero
	.hero-minimal {
		display: flex;
		min-height: 900px;
		align-items: center;
		justify-content: flex-start;
		padding-top: 120px;
		padding-bottom: 260px;
	}
	.hero-content {
		z-index: 3;
		max-width: 690px;
		margin: 0 auto;
		text-align: center;
	}
	.hero-actions { justify-content: center; }
	.seattle-outline {
		position: absolute;
		z-index: 1;
		bottom: 0;
		left: 50%;
		width: 100vw;
		height: auto;
		max-width: none;
		opacity: .78;
		filter: saturate(.62) contrast(.94);
		transform: translateX(-50%);
		pointer-events: none;
	}
	@media (max-width: 768px) {
		.hero-minimal { min-height: 820px; padding-top: 120px; padding-bottom: 220px; }
		.seattle-outline { width: 160vw; opacity: .68; }
	}
	*/
	.hero-statement {
		margin: 0 0 10px;
		color: #4f4945;
		font-family: 'Fraunces', serif;
		font-size: clamp(24px, 2.6vw, 34px);
		font-weight: 600;
		line-height: 1.2;
		letter-spacing: -0.8px;
	}
	.hero-statement + .hero-tagline {
		max-width: 590px;
		margin-right: auto;
		margin-bottom: 34px;
		margin-left: auto;
		font-size: 17px;
		line-height: 1.65;
		text-transform: none;
	}
	.footer-identity {
		display: inline-flex;
		align-items: center;
	}
	.footer-wordmark {
		display: inline-flex;
		flex-direction: column;
		color: #405047;
		font-family: 'Fraunces', serif;
		line-height: .8;
	}
	.footer-wordmark > span {
		font-size: clamp(44px, 5vw, 62px);
		font-weight: 650;
		letter-spacing: -.065em;
	}
	.footer-wordmark small {
		margin-top: 6px;
		font-family: 'Manrope', sans-serif;
		font-size: 11px;
		font-weight: 400;
		line-height: 1;
		letter-spacing: .24em;
		text-align: center;
	}

	/* Human, photo led About section */
	:global(.about-intro) {
		margin-bottom: 28px;
	}
	.illustration-band {
		min-height: 0;
		grid-template-columns: minmax(280px, .75fr) minmax(520px, 1.25fr);
		gap: clamp(44px, 6vw, 84px);
		align-items: center;
		margin-top: 20px;
		padding: 58px 58px 48px;
	}
	.illustration-copy {
		padding-top: 0;
	}
	.illustration-copy .story-lead {
		max-width: 510px;
		margin: 0 0 28px;
		color: #464541;
		font-family: 'Source Serif 4', Georgia, serif;
		font-size: clamp(26px, 2.7vw, 39px);
		font-weight: 500;
		line-height: 1.22;
		letter-spacing: -1px;
	}
	.story-lead strong {
		display: inline;
		font-weight: 650;
	}
	.illustration-copy > p:not(.story-lead) {
		max-width: 470px;
		font-size: 15px;
		line-height: 1.78;
	}
	.about-photo-frame,
	.about-photo-frame:hover {
		position: relative;
		margin: 0;
		padding: 9px 9px 16px;
		border: 1px solid rgba(100, 88, 76, .08);
		border-radius: 2px;
		background: #fffdf8;
		box-shadow: 0 22px 52px rgba(67, 57, 49, .13);
		transform: rotate(.7deg);
	}
	.about-photo-frame::before {
		position: absolute;
		top: -13px;
		left: 50%;
		width: 82px;
		height: 25px;
		background: rgba(223, 210, 188, .72);
		content: '';
		transform: translateX(-50%) rotate(-1.5deg);
	}
	.about-photo-crop {
		position: relative;
		aspect-ratio: 3 / 2;
		overflow: hidden;
		border-radius: 0;
	}
	.about-photo-crop img {
		position: static;
		width: 100%;
		height: 100%;
		max-width: 100%;
		object-fit: cover;
		filter: saturate(.84) contrast(.97);
		transform: none;
	}
	@media (max-width: 900px) {
		.illustration-band { grid-template-columns: 1fr; padding: 46px 36px 38px; }
		.about-photo-frame { width: min(680px, 100%); }
	}
	@media (max-width: 620px) {
		:global(.about-intro) { margin-bottom: 18px; }
		.illustration-band { gap: 34px; margin-top: 10px; padding: 36px 20px 28px; }
		.illustration-copy .story-lead { font-size: 27px; }
	}

	/* Typography led Vision and Mission */
	.belief-section {
		position: relative;
		z-index: 0;
		margin-top: 130px;
		padding: 118px 0 128px;
	}
	.belief-section::before {
		position: absolute;
		z-index: -1;
		inset: 0 50%;
		width: 100vw;
		background: #f4f6f1;
		content: '';
		transform: translateX(-50%);
	}
	.belief-heading {
		margin: 0 0 86px;
		text-align: left;
	}
	.belief-heading h2 {
		max-width: 720px;
		font-size: clamp(52px, 6vw, 78px);
		line-height: .98;
	}
	.about-grid {
		display: grid;
		max-width: 1160px;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: clamp(70px, 10vw, 150px);
		margin: 0 auto;
	}
	.about-card,
	.about-card:first-child,
	.about-card:last-child {
		display: block;
		min-height: 0;
		padding: 0;
		border: 0;
		background: transparent;
		box-shadow: none;
	}
	.about-card:hover,
	.about-card:first-child:hover,
	.about-card:last-child:hover {
		padding: 0;
		background: transparent;
		box-shadow: none;
		transform: none;
	}
	.belief-label {
		display: block;
		margin-bottom: 34px;
	}
	.belief-label .about-label {
		display: inline-block;
		position: relative;
		padding-bottom: 9px;
		color: #7d5949;
		font-size: 10px;
		letter-spacing: .22em;
	}
	.belief-label .about-label::after {
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		height: 1px;
		background: #bd7658;
		content: '';
		transform: scaleX(0);
		transform-origin: left;
		transition: transform 1s cubic-bezier(.22, 1, .36, 1) .35s;
	}
	:global(.about-card.visible) .about-label::after {
		transform: scaleX(1);
	}
	.belief-copy {
		padding: 0;
	}
	.belief-copy h3 {
		max-width: 540px;
		margin: 0 0 32px;
		color: #39423c;
		font-family: 'Fraunces', serif;
		font-size: clamp(46px, 5.2vw, 70px);
		font-weight: 580;
		line-height: 1.02;
		letter-spacing: -.055em;
	}
	.belief-copy .about-description {
		max-width: 490px;
		color: #666c65;
		font-size: 16px;
		line-height: 1.78;
	}
	@media (max-width: 800px) {
		.belief-section { margin-top: 90px; padding: 88px 0 98px; }
		.belief-heading { margin-bottom: 64px; }
		.about-grid { grid-template-columns: 1fr; gap: 86px; }
		.belief-copy h3 { font-size: clamp(44px, 12vw, 62px); }
	}
	@media (prefers-reduced-motion: reduce) {
		.belief-label .about-label::after { transform: scaleX(1); transition: none; }
	}

	/* Unified editorial About section */
	.about {
		padding-top: 150px;
	}
	.illustration-band {
		grid-template-columns: minmax(340px, .85fr) minmax(520px, 1.15fr);
		gap: clamp(60px, 8vw, 110px);
		align-items: center;
		margin: 0;
		padding: 0 0 145px;
		border: 0;
		border-radius: 0;
		background: transparent;
		box-shadow: none;
	}
	.illustration-copy h2 {
		max-width: 570px;
		margin: 12px 0 22px;
		color: #3d403c;
		font-family: 'Fraunces', serif;
		font-size: clamp(52px, 6vw, 76px);
		font-weight: 600;
		line-height: .98;
		letter-spacing: -.055em;
	}
	.illustration-copy .story-lead {
		margin-bottom: 26px;
		font-size: clamp(24px, 2.45vw, 34px);
		line-height: 1.27;
	}
	.about-photo-frame,
	.about-photo-frame:hover {
		padding: 7px;
		border: 1px solid rgba(78, 75, 68, .08);
		border-radius: 12px;
		background: var(--warm-surface);
		box-shadow: 0 20px 50px rgba(59, 56, 49, .1);
		transform: none;
	}
	.about-photo-frame::before {
		display: none;
	}
	.about-photo-crop {
		aspect-ratio: 4 / 3;
		border-radius: 7px;
	}
	.about-photo-crop img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center;
		transform: scale(1.3);
	}
	@media (max-width: 900px) {
		.about { padding-top: 100px; }
		.illustration-band { grid-template-columns: 1fr; gap: 54px; padding-bottom: 105px; }
		.illustration-copy { max-width: 650px; }
		.about-photo-frame { width: 100%; }
	}
	@media (max-width: 620px) {
		.illustration-band { gap: 42px; padding: 0 0 84px; }
		.illustration-copy h2 { font-size: 52px; }
		.about-photo-frame { padding: 5px; border-radius: 9px; }
	}

	/* Unified KAWAN design system */
	:global(body) {
		--warm-cream: #f7f3ea;
		--warm-beige: #f0eadf;
		--warm-surface: #fbf8f2;
		color: #343a35;
		background: var(--warm-cream);
		font-family: 'Manrope', sans-serif;
	}
	:global(main) { background: var(--warm-cream); }
	h1, :global(blockquote) {
		font-family: 'Fraunces', serif;
	}
	h2, h3,
	.hero-statement,
	.illustration-copy h2,
	.belief-heading h2,
	.belief-copy h3,
	.journey-section-heading h2,
	.program-card h3,
	.cta-content h2 {
		font-family: 'Source Serif 4', Georgia, serif;
	}
	.illustration-copy h2,
	.belief-heading h2,
	.journey-section-heading h2,
	.events-heading h2,
	.moments-heading h3,
	.cta-content h2 {
		font-weight: 650;
		letter-spacing: -.04em;
		text-rendering: optimizeLegibility;
	}
	.about-eyebrow, .about-label {
		color: #8a6250;
		font-family: 'Manrope', sans-serif;
		font-size: 10px;
		font-weight: 700;
		letter-spacing: .2em;
		text-transform: uppercase;
	}
	.about-eyebrow {
		position: relative;
		z-index: 2;
		font-size: 15px;
	}
	.illustration-copy h2,
	.belief-heading h2,
	.journey-section-heading h2,
	.events-heading h2,
	.moments-heading h3,
	.cta-content h2 {
		position: relative;
		z-index: 1;
	}
	.button, :global(.button.gold) {
		min-height: 50px;
		padding: 0 22px;
		border: 0;
		border-radius: 6px;
		color: #fffdf8;
		background: #46564b;
		box-shadow: none;
		font-family: 'Manrope', sans-serif;
		font-size: 12px;
		font-weight: 700;
		letter-spacing: .04em;
	}
	.button:hover, :global(.button.gold):hover { background: #35433a; box-shadow: none; transform: translateY(-2px); }
	.header-actions {
		display: flex;
		align-items: center;
		gap: 28px;
	}
	.site-header nav a,
	.site-header .desktop-cta {
		font-size: 15px;
	}
	.language-toggle {
		display: inline-flex;
		align-items: center;
		gap: 6px;
		color: rgba(64, 80, 71, .38);
		font: 700 15px 'Manrope', sans-serif;
		letter-spacing: .1em;
	}
	.language-toggle button {
		padding: 5px 2px;
		border: 0;
		color: #817b73;
		background: transparent;
		font: inherit;
		cursor: pointer;
		transition: color .2s ease;
	}
	.language-toggle button:hover,
	.language-toggle button.active { color: #405047; }
	.language-toggle button.active { text-decoration: underline; text-decoration-color: #b7785d; text-underline-offset: 5px; }

	.hero {
		position: relative;
		overflow: hidden;
		min-height: 790px;
		background: #eae5d9;
	}
	.hero::before, .hero::after { display: none; }
	.hero-minimal {
		position: relative;
		display: flex;
		min-height: 790px;
		align-items: center;
		justify-content: center;
		padding-top: 142px;
		padding-bottom: 96px;
	}
	.hero-content {
		position: relative;
		z-index: 2;
		max-width: 760px;
		text-align: center;
	}
	.hero-content > * {
		opacity: 0;
		animation: hero-copy-in .75s cubic-bezier(.2,.7,.2,1) both;
	}
	.hero-content .hero-kicker { animation-delay: .08s; }
	.hero-content h1 { animation-delay: .2s; }
	.hero-content .hero-statement { animation-delay: .34s; }
	.hero-content .hero-tagline { animation-delay: .48s; }
	.hero-content .hero-actions { animation-delay: .62s; }
	.hero-kicker { position: relative; z-index: 2; margin: 0 0 10px; color: #846351; font-size: 15px; font-weight: 700; letter-spacing: .2em; text-transform: uppercase; }
	.hero h1 { position: relative; z-index: 1; margin: 0; font-size: clamp(88px, 12vw, 152px); line-height: .85; letter-spacing: -.065em; text-transform: none; }
	.hero .kawan-script { padding: 0; color: #405047; font-family: 'Fraunces', serif; font-size: 1em; font-style: normal; font-weight: 650; letter-spacing: -.065em; text-transform: none; }
	.hero .kawan-script::before { display: none; }
	.hero-statement { margin: 32px 0 13px; font-size: clamp(30px, 3.3vw, 43px); font-weight: 550; letter-spacing: -.035em; }
	.hero-statement + .hero-tagline { max-width: 620px; margin: 0 auto 32px; color: #66635e; font-size: 15px; line-height: 1.75; }
	.hero-actions { justify-content: center; margin: 0; }
	.hero-illustrations {
		position: absolute;
		z-index: 1;
		inset: 92px 0 18px;
		pointer-events: none;
	}
	.hero-illustration {
		--hero-art-opacity: .96;
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: contain;
		opacity: calc(var(--hero-art-opacity) * var(--hero-scroll-fade));
		pointer-events: none;
		mask-image: linear-gradient(90deg, #000, #000);
		mask-repeat: no-repeat;
		mask-size: 0% 100%;
		animation: illustration-reveal .85s cubic-bezier(.2,.7,.2,1) forwards;
	}
	.illustration-space-needle { clip-path: inset(0 50% 50% 0); animation-delay: .72s; }
	.illustration-board-game { clip-path: inset(0 0 50% 50%); animation-delay: .9s; }
	.illustration-water-taxi { clip-path: inset(50% 50% 0 0); animation-delay: 1.08s; }
	.illustration-hiking { clip-path: inset(50% 0 0 50%); animation-delay: 1.26s; }
	.hero-illustration-mobile { display: none; }
	.hero-actions .hero-button {
		min-width: 132px;
		padding: 0 30px;
		border: 1px solid rgba(255,255,255,.2);
		border-radius: 999px;
		box-shadow: 0 7px 18px rgba(48,60,51,.12);
		letter-spacing: .025em;
		transition: background .25s ease, box-shadow .25s ease, transform .25s ease;
	}
	.hero-actions .hero-button:hover { background: #35433a; box-shadow: 0 10px 24px rgba(48,60,51,.18); transform: translateY(-2px); }
	@keyframes hero-copy-in { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: none; } }
	@keyframes illustration-reveal { to { mask-size: 100% 100%; } }

	.about { padding-top: 145px; padding-bottom: 0; background: var(--warm-cream); }
	.illustration-band { gap: clamp(62px, 8vw, 110px); padding-bottom: 145px; }
	.about-photo-frame, .about-photo-frame:hover {
		padding: 0;
		border: 0;
		border-radius: 10px;
		background: transparent;
		box-shadow: 0 20px 52px rgba(55,52,46,.1);
		transform: none;
	}
	.about-photo-crop { border-radius: 10px; }
	.illustration-copy > p:not(.story-lead) { font-weight: 500; }
	.illustration-copy > p strong { font-weight: 600; }

	.belief-section {
		position: relative;
		margin-top: 0;
		padding: clamp(104px, 10vw, 148px) 0 clamp(112px, 11vw, 158px);
	}
	.belief-section::before { background: var(--warm-beige); }
	.belief-heading {
		max-width: 760px;
		margin: 0 auto clamp(72px, 8vw, 108px);
		text-align: center;
	}
	.belief-heading h2 {
		position: relative;
		width: fit-content;
		margin: 10px auto 0;
		padding-bottom: 18px;
		font-size: clamp(54px, 6vw, 78px);
	}
	.belief-heading h2::after {
		position: absolute;
		bottom: 0;
		left: 50%;
		width: 74px;
		height: 7px;
		border-top: 2px solid rgba(189, 118, 88, .52);
		border-radius: 50%;
		content: '';
		transform: translateX(-50%) rotate(-2deg);
	}
	.belief-section .belief-grid {
		display: grid;
		max-width: 1160px;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: clamp(72px, 10vw, 150px);
		align-items: start;
		margin: 0 auto;
		overflow: visible;
		border: 0;
		border-radius: 0;
		background: transparent;
	}
	.belief-section .belief-block,
	.belief-section .belief-block:first-child,
	.belief-section .belief-block:last-child {
		display: flex;
		min-height: 0;
		flex-direction: column;
		padding: 0;
		border: 0;
		border-radius: 0;
		background: transparent;
		box-shadow: none;
	}
	.belief-section .belief-block:hover,
	.belief-section .belief-block:first-child:hover,
	.belief-section .belief-block:last-child:hover {
		padding: 0;
		background: transparent;
		box-shadow: none;
		transform: none;
	}
	.belief-label { margin: 0 0 30px; }
	.belief-label .about-label { color: #8a6250; font-size: 15px; }
	.belief-copy h3 {
		max-width: 540px;
		margin-bottom: 26px;
		font-size: clamp(40px, 4vw, 57px);
		font-weight: 600;
		line-height: 1.06;
		letter-spacing: -.045em;
	}
	.belief-copy .about-description {
		max-width: 500px;
		color: #696761;
		font-size: 15px;
		line-height: 1.8;
	}
	@media (max-width: 800px) {
		.belief-section { padding: 96px 0 112px; }
		.belief-heading { margin-bottom: 72px; }
		.belief-section .belief-grid { grid-template-columns: 1fr; gap: 72px; }
		.belief-section .belief-block,
		.belief-section .belief-block:first-child,
		.belief-section .belief-block:last-child {
			min-height: 0;
			padding: 0;
			border: 0;
		}
		.belief-section .belief-block:hover,
		.belief-section .belief-block:first-child:hover,
		.belief-section .belief-block:last-child:hover { padding: 0; }
		.belief-copy .about-description { max-width: 600px; }
	}

	.programs.section-wrap {
		display: block;
		box-sizing: border-box;
		padding-top: clamp(86px, 9vw, 124px);
		padding-bottom: clamp(90px, 9vw, 126px);
		background: var(--warm-cream);
	}
	.journey-section-heading {
		max-width: 760px;
		margin: 0 auto;
		text-align: center;
	}
	.journey-section-heading h2 {
		margin: 6px 0 8px;
		color: #34463b;
		font-size: clamp(47px, 4.7vw, 66px);
		font-weight: 650;
		line-height: 1.02;
		letter-spacing: -.045em;
	}
	.journey-section-heading > p:last-child {
		max-width: 620px;
		margin: 0 auto;
		color: #706b64;
		font-family: 'Source Serif 4', Georgia, serif;
		font-size: clamp(16px, 1.25vw, 19px);
		font-style: italic;
		line-height: 1.55;
	}
	.program-grid.minimal.support-journey {
		display: grid;
		width: 100%;
		max-width: 1280px;
		grid-template-columns: 1fr;
		gap: 16px;
		margin: clamp(48px, 5vw, 68px) auto 0;
	}
	.program-grid.minimal.support-journey > .support-stop {
		grid-column: 1 / -1;
	}
	.support-stop {
		position: relative;
		display: grid;
		width: 100%;
		min-width: 0;
		min-height: 210px;
		grid-template-columns: minmax(245px, .82fr) minmax(330px, 1.2fr) minmax(265px, .9fr);
		gap: 0;
		align-items: center;
		margin: 0;
		padding: 0;
		overflow: hidden;
		border: 1px solid rgba(105, 97, 87, .08);
		border-radius: 20px;
		background: #f8f4ec;
		box-shadow: none;
		isolation: isolate;
		transition: border-color .28s ease, transform .28s ease;
	}
	.support-stop:nth-child(2) { background: #e9efef; }
	.support-stop:nth-child(3) { background: #f7e5dc; }
	.support-stop:nth-child(4) { background: #f5efdf; }
	.support-stop:hover { border-color: rgba(93, 91, 83, .18); box-shadow: none; }
	:global(.support-stop.visible:hover) { transform: translateY(-2px); }
	.support-visual {
		position: relative;
		z-index: 1;
		grid-column: 1;
		grid-row: 1;
		width: 100%;
		height: 100%;
		min-height: 210px;
		margin: 0;
		overflow: hidden;
		border-radius: 0;
		pointer-events: none;
	}
	.support-visual img {
		display: block;
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: left center;
		opacity: .92;
		filter: saturate(.72) contrast(.98);
		mix-blend-mode: multiply;
		transform: scale(1.08);
		transition: opacity .35s ease, transform .55s cubic-bezier(.2,.7,.2,1);
	}
	.support-stop:nth-child(even) .support-visual {
		grid-column: 3;
	}
	.support-stop:nth-child(even) .support-visual img { object-position: right center; }
	.support-stop:hover .support-visual img { opacity: 1; transform: scale(1.1); }
	.support-copy {
		position: relative;
		z-index: 2;
		grid-column: 2;
		grid-row: 1;
		width: 100%;
		margin: 0;
		padding: clamp(28px, 3vw, 46px);
		background: transparent;
	}
	.support-stop:nth-child(even) .support-copy { grid-column: 1; }
	.support-copy h3 {
		position: relative;
		width: fit-content;
		margin: 0 0 8px;
		padding-bottom: 7px;
		color: #39443d;
		font-family: 'Source Serif 4', Georgia, serif;
		font-size: clamp(32px, 3vw, 44px);
		font-weight: 650;
		line-height: 1.1;
		letter-spacing: -.035em;
	}
	.support-copy h3::after {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 46px;
		height: 2px;
		border-radius: 99px;
		background: #777b75;
		content: '';
		transform: rotate(-1deg);
	}
	.support-copy > p { margin: 0; color: #74736e; font-size: 14px; line-height: 1.58; }
	.support-copy > p:first-of-type { color: #515a53; font-weight: 650; }
	.support-copy > .support-details { margin-top: 8px; color: #74736e; font-weight: 500; }
	.support-activities {
		display: grid;
		grid-column: 3;
		grid-row: 1;
		gap: 10px;
		margin: 0;
		padding: clamp(28px, 3vw, 46px);
		list-style: none;
	}
	.support-stop:nth-child(even) .support-activities { grid-column: 2; }
	.support-activities li {
		display: flex;
		align-items: center;
		gap: 13px;
		padding: 0;
		border: 0;
		border-radius: 0;
		color: #46534a;
		background: transparent;
		font-size: 14px;
		font-weight: 650;
		line-height: 1.45;
	}
	.support-activities li::before {
		display: block;
		width: 18px;
		height: 18px;
		flex: 0 0 auto;
		color: #73807a;
		content: '✦';
		font: 700 16px/18px 'Source Serif 4', Georgia, serif;
		text-align: center;
	}
	.support-activities li:nth-child(1)::before { content: '✈'; }
	.support-activities li:nth-child(2)::before { content: '⌂'; }
	.support-activities li:nth-child(3)::before { content: '◇'; }
	.support-activities li:nth-child(4)::before { content: '✦'; }
	.support-activities li:nth-child(5)::before { content: '○'; }
	.support-activities li:nth-child(6)::before { content: '▣'; }
	.support-stop:nth-child(2) .support-activities li::before { color: #657e8b; }
	.support-stop:nth-child(3) .support-activities li::before { color: #b76f54; }
	.support-stop:nth-child(4) .support-activities li::before { color: #728077; }
	@media (max-width: 960px) {
		.support-stop { grid-template-columns: minmax(200px, .75fr) minmax(300px, 1fr); gap: 0; }
		.support-stop .support-visual,
		.support-stop:nth-child(even) .support-visual { grid-column: 1; grid-row: 1 / 3; }
		.support-stop .support-copy,
		.support-stop:nth-child(even) .support-copy { grid-column: 2; grid-row: 1; align-self: end; padding-bottom: 14px; }
		.support-stop .support-activities,
		.support-stop:nth-child(even) .support-activities { grid-column: 2; grid-row: 2; align-self: start; padding-top: 8px; }
	}
	@media (max-width: 700px) {
		.programs.section-wrap { padding: 84px 24px 92px; }
		.support-stop { grid-template-columns: 1fr; gap: 0; padding: 0; }
		.support-stop .support-visual,
		.support-stop:nth-child(even) .support-visual { grid-column: 1; grid-row: 1; height: 210px; min-height: 210px; }
		.support-stop .support-copy,
		.support-stop:nth-child(even) .support-copy { grid-column: 1; grid-row: 2; padding: 28px 26px 12px; }
		.support-stop .support-activities,
		.support-stop:nth-child(even) .support-activities { grid-column: 1; grid-row: 3; padding: 12px 26px 30px; }
	}

	/* Restored illustrated 2x2 support cards */
	.programs.section-wrap {
		display: flex;
		min-height: 100svh;
		box-sizing: border-box;
		flex-direction: column;
		padding: 52px 5.5vw 58px;
		background: var(--warm-cream);
	}
	.program-grid.minimal.support-journey {
		display: grid;
		flex: 1;
		width: 100%;
		max-width: none;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		grid-template-rows: repeat(2, minmax(232px, 1fr));
		gap: 18px;
		margin: 35px 0 0;
	}
	.program-grid.minimal.support-journey > .support-stop,
	.support-stop,
	.support-stop:nth-child(2),
	.support-stop:nth-child(3),
	.support-stop:nth-child(4) {
		position: relative;
		display: flex;
		width: 100%;
		min-width: 0;
		min-height: 0;
		grid-column: auto;
		align-items: center;
		margin: 0;
		padding: clamp(18px, 1.5vw, 24px);
		overflow: hidden;
		border: 1px solid rgba(105, 97, 87, .16);
		border-radius: 14px;
		background: rgba(251, 248, 242, .78);
		box-shadow: none;
		transition: border-color .28s ease, background-color .28s ease, transform .28s ease;
	}
	.support-stop + .support-stop { border: 1px solid rgba(105, 97, 87, .12); }
	.support-stop:hover,
	.support-stop:nth-child(2):hover,
	.support-stop:nth-child(3):hover,
	.support-stop:nth-child(4):hover {
		border-color: rgba(93, 91, 83, .22);
		background: rgba(251, 248, 242, .94);
		box-shadow: none;
	}
	:global(.support-stop.visible:hover) { transform: translateY(-3px); }
	.support-stop .support-visual,
	.support-stop:nth-child(even) .support-visual {
		position: absolute;
		z-index: 1;
		inset: 0;
		display: grid;
		width: 100%;
		height: 100%;
		min-height: 0;
		margin: 0;
		overflow: visible;
		border-radius: 0;
		place-items: center;
		pointer-events: none;
	}
	.support-stop .support-visual img,
	.support-stop:nth-child(even) .support-visual img {
		position: relative;
		display: block;
		width: 100%;
		height: 100%;
		max-height: none;
		object-fit: cover;
		object-position: center;
		opacity: .72;
		filter: saturate(.72) contrast(.98);
		mix-blend-mode: multiply;
		transform: scale(1.01);
		transition: opacity .35s ease, transform .55s cubic-bezier(.2,.7,.2,1);
	}
	.support-stop:hover .support-visual img { opacity: .82; transform: scale(1.015); }
	.support-stop .support-copy,
	.support-stop:nth-child(even) .support-copy {
		position: relative;
		z-index: 2;
		width: 59%;
		max-width: none;
		margin-right: 0;
		margin-left: auto;
		padding: clamp(20px, 1.7vw, 28px);
		border-radius: 12px;
		background: rgba(251, 248, 242, .92);
		backdrop-filter: blur(3px);
	}
	.support-stop:nth-child(even) .support-copy { margin-right: auto; margin-left: 0; }
	.support-copy h3 { font-size: clamp(27px, 2.15vw, 35px); }
	.support-copy > p { font-size: 13px; line-height: 1.5; }
	.support-activities {
		display: flex;
		flex-wrap: wrap;
		gap: 7px 8px;
		margin: 10px 0 0;
		padding: 0;
		list-style: none;
	}
	.support-activities li {
		display: inline-flex;
		align-items: center;
		padding: 7px 12px;
		border: 1px solid rgba(102, 99, 92, .07);
		border-radius: 18px;
		color: #46534a;
		background: rgba(117, 108, 96, .035);
		font-size: 11px;
		font-weight: 600;
		line-height: 1.45;
	}
	.support-activities li::before { display: none; content: none; }
	@media (max-width: 960px) {
		.programs.section-wrap { display: block; min-height: 0; padding: 86px 5vw 94px; }
		.program-grid.minimal.support-journey { grid-template-columns: repeat(2, minmax(0, 1fr)); grid-template-rows: none; grid-auto-rows: auto; gap: 18px; margin-top: 44px; }
		.program-grid.minimal.support-journey > .support-stop,
		.support-stop,
		.support-stop:nth-child(2),
		.support-stop:nth-child(3),
		.support-stop:nth-child(4) { grid-column: auto; display: grid; grid-template-columns: 1fr; padding: 24px; }
		.support-stop .support-visual,
		.support-stop:nth-child(even) .support-visual { position: relative; inset: auto; grid-column: 1; grid-row: 1; width: 100%; height: 180px; min-height: 0; }
		.support-stop .support-copy,
		.support-stop:nth-child(even) .support-copy { grid-column: 1; grid-row: 2; width: 100%; max-width: 540px; margin: 0; padding: clamp(20px, 1.7vw, 28px); }
	}
	@media (max-width: 700px) {
		.programs.section-wrap { padding: 84px 24px 92px; }
		.program-grid.minimal.support-journey { grid-template-columns: 1fr; }
		.support-stop .support-visual,
		.support-stop:nth-child(even) .support-visual { height: 220px; }
	}

	.community-photo-break {
		position: relative;
		overflow: hidden;
		width: min(1400px, calc(100% - 48px));
		height: clamp(430px, 64vw, 720px);
		margin: 0 auto;
		border-radius: 10px;
	}
	.community-photo-break img { width: 100%; height: 100%; object-fit: cover; object-position: center; filter: saturate(.84) contrast(.97); }
	.community-photo-break::after { position: absolute; inset: 55% 0 0; background: linear-gradient(transparent, rgba(29,36,31,.64)); content: ''; }
	.community-photo-break p { position: absolute; z-index: 2; right: 7%; bottom: 7%; max-width: 620px; margin: 0; color: white; font-family: 'Source Serif 4', Georgia, serif; font-size: clamp(32px, 4.6vw, 64px); font-weight: 650; line-height: 1.05; letter-spacing: -.035em; text-align: right; }

	.stories { padding-top: 145px; padding-bottom: 145px; background: var(--warm-beige); }
	:global(.story-card) { border: 1px solid rgba(64,77,66,.11); border-radius: 8px; box-shadow: none; }
	:global(.student) img { filter: saturate(.82); }

	/* Events */
	.events { padding-top: 145px; padding-bottom: 150px; }
	.events-heading { max-width: 760px; margin-bottom: 82px; }
	.events-heading h2 { margin: 10px 0 22px; color: #3e4841; font-family: 'Source Serif 4', Georgia, serif; font-size: clamp(64px, 8vw, 104px); line-height: .9; letter-spacing: -.055em; }
	.events-heading h3 { margin: -4px 0 18px; color: #4b554e; font-family: 'Source Serif 4', Georgia, serif; font-size: clamp(25px, 2.7vw, 34px); font-weight: 600; letter-spacing: -.025em; }
	.events-heading > p:last-child { max-width: 650px; margin: 0; color: #696b66; font-size: 16px; line-height: 1.75; }
	.events-feature { display: grid; grid-template-columns: minmax(320px, .78fr) minmax(520px, 1.22fr); gap: clamp(42px, 6vw, 82px); align-items: start; }
	.event-calendar { padding-top: 6px; }
	.calendar-heading { display: flex; align-items: flex-end; justify-content: space-between; gap: 24px; margin-bottom: 34px; padding-bottom: 20px; border-bottom: 1px solid rgba(65,77,67,.15); }
	.calendar-heading p { margin: 0; color: #93654f; font-size: 10px; font-weight: 700; letter-spacing: .17em; text-transform: uppercase; }
	.calendar-heading h3 { margin: 0; color: #414b44; font-family: 'Source Serif 4', Georgia, serif; font-size: 28px; font-weight: 550; letter-spacing: -.03em; }
	.calendar-grid { display: grid; grid-template-columns: repeat(7, 1fr); }
	.calendar-weekdays { margin-bottom: 12px; }
	.calendar-weekdays span { color: #8b8c86; font-size: 9px; font-weight: 700; letter-spacing: .08em; text-align: center; text-transform: uppercase; }
	.calendar-dates { row-gap: 8px; }
	.calendar-dates > span,
	.calendar-dates > button { display: grid; width: 42px; height: 42px; margin: auto; place-items: center; border: 0; border-radius: 50%; color: #5f625d; background: transparent; font: 500 12px 'Manrope', sans-serif; }
	.calendar-dates > span.empty { visibility: hidden; }
	.calendar-dates > button { position: relative; color: #435248; cursor: pointer; transition: color .24s ease, background .24s ease, transform .24s ease; }
	.calendar-dates > button::after { position: absolute; bottom: 5px; width: 3px; height: 3px; border-radius: 50%; background: #a76f54; content: ''; }
	.calendar-dates > button:hover { background: #ebece5; transform: translateY(-1px); }
	.calendar-dates > button.active { color: #fff; background: #4b5b50; }
	.calendar-dates > button.active::after { background: #e8c9b8; }
	.featured-event { overflow: hidden; border: 1px solid rgba(65,77,67,.1); border-radius: 8px; background: var(--warm-surface); }
	.featured-event-photo { overflow: hidden; aspect-ratio: 16 / 9; background: #e8e7df; }
	.featured-event-photo img { width: 100%; height: 100%; object-fit: cover; object-position: center; filter: saturate(.86) contrast(.97); transition: transform .55s ease; }
	.featured-event:hover .featured-event-photo img { transform: scale(1.015); }
	.featured-event-copy { padding: clamp(28px, 4vw, 46px); }
	.event-date { display: flex; gap: 14px; margin: 0 0 14px; color: #93654f; font-size: 10px; font-weight: 700; letter-spacing: .13em; text-transform: uppercase; }
	.featured-event-copy h3 { margin: 0 0 15px; color: #414a43; font-family: 'Source Serif 4', Georgia, serif; font-size: clamp(38px, 4vw, 56px); line-height: 1; letter-spacing: -.04em; }
	.featured-event-copy > p:not(.event-date) { max-width: 590px; margin: 0 0 26px; color: #696b66; font-size: 14px; line-height: 1.7; }
	.featured-event-copy .button { width: fit-content; cursor: pointer; }
	.moments-heading { max-width: 680px; margin: 150px 0 58px; }
	.moments-heading h3 { margin: 10px 0 18px; color: #414a43; font-family: 'Source Serif 4', Georgia, serif; font-size: clamp(50px, 6vw, 76px); line-height: .98; letter-spacing: -.045em; }
	.moments-heading > p:last-child { margin: 0; color: #696b66; font-size: 15px; line-height: 1.75; }
	.moments-gallery { display: grid; grid-template-columns: repeat(12, 1fr); grid-template-rows: 300px 300px; gap: 16px; }
	.moment { position: relative; overflow: hidden; min-width: 0; margin: 0; border-radius: 7px; background: #e6e5dd; }
	.moment-wide { grid-column: 1 / 6; grid-row: 1 / 3; }
	.moment-tall { grid-column: 6 / 13; grid-row: 1; }
	.moment-small { grid-column: 6 / 9; grid-row: 2; }
	.moment-small:last-child { grid-column: 9 / 13; }
	.hiking-slide { width: 100%; height: 100%; }
	.hiking-slide img { animation: hiking-photo-in .45s ease both; }
	.moment img { width: 100%; height: 100%; object-fit: cover; filter: saturate(.82) contrast(.96); transition: transform .55s ease, filter .55s ease; }
	.moment-wide img { object-position: center; }
	.moment-tall img { object-position: center 42%; }
	.moment figcaption { position: absolute; z-index: 2; right: 0; bottom: 0; left: 0; display: flex; align-items: flex-end; justify-content: space-between; gap: 20px; padding: 52px 24px 22px; color: #fff; background: linear-gradient(transparent, rgba(31,38,33,.72)); }
	.moment figcaption strong { font-family: 'Fraunces', serif; font-size: 23px; font-weight: 550; }
	.moment figcaption span { font-size: 9px; font-weight: 650; letter-spacing: .1em; text-transform: uppercase; }
	.moment:hover img { filter: saturate(.9) contrast(.98); transform: scale(1.018); }
	.slide-arrow {
		position: absolute;
		z-index: 4;
		top: 50%;
		display: grid;
		width: 38px;
		height: 38px;
		padding: 0 0 3px;
		place-items: center;
		border: 1px solid rgba(255,255,255,.42);
		border-radius: 50%;
		color: #fff;
		background: rgba(45,54,47,.38);
		font: 400 26px/1 Georgia, serif;
		cursor: pointer;
		transform: translateY(-50%);
		backdrop-filter: blur(5px);
		transition: background .24s ease, transform .24s ease;
	}
	.slide-previous { left: 18px; }
	.slide-next { right: 18px; }
	.slide-arrow:hover { background: rgba(45,54,47,.62); transform: translateY(-50%) scale(1.04); }
	.slide-dots { position: absolute; z-index: 4; right: 22px; bottom: 72px; display: flex; gap: 7px; }
	.slide-dots button { width: 7px; height: 7px; padding: 0; border: 1px solid rgba(255,255,255,.75); border-radius: 50%; background: rgba(255,255,255,.18); cursor: pointer; transition: background .22s ease, transform .22s ease; }
	.slide-dots button.active { background: #fff; transform: scale(1.15); }
	@keyframes hiking-photo-in { from { opacity: .25; } to { opacity: 1; } }

	.cta-minimal { padding: 150px 0; background: var(--warm-cream); }
	.cta-content { max-width: 820px; margin: 0 auto; }
	.cta-content h2 { margin: 12px 0 24px; font-size: clamp(56px, 7vw, 88px); line-height: .98; }
	.cta-content > p:not(.about-eyebrow) { max-width: 620px; margin: 0 auto 12px; color: #666b65; font-size: 16px; line-height: 1.75; }
	.cta-content > p:not(.about-eyebrow):last-of-type { margin-bottom: 34px; }
	.cta-actions { display: flex; align-items: center; justify-content: center; gap: 28px; }

	.connect-modal-backdrop {
		position: fixed;
		z-index: 100;
		inset: 0;
		display: grid;
		padding: 24px;
		place-items: center;
		background: rgba(38, 43, 39, .48);
		backdrop-filter: blur(5px);
		animation: modal-backdrop-in .25s ease both;
	}
	.connect-modal {
		position: relative;
		width: min(540px, 100%);
		padding: clamp(38px, 6vw, 58px);
		border: 1px solid rgba(65, 77, 67, .11);
		border-radius: 10px;
		background: var(--warm-surface);
		box-shadow: 0 26px 70px rgba(35, 41, 36, .2);
		animation: modal-content-in .38s cubic-bezier(.2,.7,.2,1) both;
	}
	.connect-modal-close {
		position: absolute;
		top: 20px;
		right: 22px;
		padding: 4px 0;
		border: 0;
		border-bottom: 1px solid rgba(60, 70, 62, .35);
		color: #626860;
		background: transparent;
		font: 650 10px 'Manrope', sans-serif;
		letter-spacing: .08em;
		text-transform: uppercase;
		cursor: pointer;
	}
	.connect-form-heading h2,
	.connect-confirmation h2 {
		margin: 10px 0 16px;
		color: #3e4841;
		font-family: 'Source Serif 4', Georgia, serif;
		font-size: clamp(38px, 6vw, 52px);
		font-weight: 650;
		line-height: 1;
		letter-spacing: -.04em;
	}
	.connect-form-heading > p:last-child,
	.connect-confirmation > p:not(.about-eyebrow) { margin: 0 0 28px; color: #696b66; font-size: 14px; line-height: 1.7; }
	.connect-form { display: grid; gap: 10px; }
	.connect-form label { margin-top: 8px; color: #4f5851; font-size: 11px; font-weight: 700; letter-spacing: .06em; }
	.connect-form input {
		width: 100%;
		height: 52px;
		padding: 0 15px;
		border: 1px solid rgba(65, 77, 67, .2);
		border-radius: 6px;
		outline: none;
		color: #343a35;
		background: var(--warm-surface);
		font: 500 14px 'Manrope', sans-serif;
		transition: border-color .22s ease, box-shadow .22s ease;
	}
	.connect-form input:focus { border-color: #65766a; box-shadow: 0 0 0 3px rgba(101, 118, 106, .1); }
	.connect-form input::placeholder { color: #9a9b95; }
	.phone-field { width: 100%; }
	:global(.phone-field .iti) {
		width: 100%;
		--iti-border-color: rgba(65, 77, 67, .16);
		--iti-dropdown-bg: #fbf8f2;
		--iti-hover-color: rgba(101, 118, 106, .09);
	}
	:global(.phone-field .iti__country-container) { padding: 1px; }
	:global(.phone-field .iti__selected-country) {
		padding: 0 12px;
		border-radius: 5px 0 0 5px;
		color: #485149;
		font-family: 'Manrope', sans-serif;
		transition: background .2s ease;
	}
	:global(.phone-field .iti__selected-dial-code) { margin-left: 8px; font-size: 13px; font-weight: 650; }
	:global(.phone-field .iti__dropdown-content) {
		z-index: 110;
		border: 1px solid rgba(65, 77, 67, .16);
		border-radius: 7px;
		background: var(--warm-surface);
		box-shadow: 0 16px 38px rgba(35, 41, 36, .16);
		font-family: 'Manrope', sans-serif;
	}
	:global(.phone-field .iti__search-input) {
		height: 42px;
		border: 0;
		border-bottom: 1px solid rgba(65, 77, 67, .14);
		border-radius: 0;
		box-shadow: none;
	}
	:global(.phone-field .iti__country) { padding-block: 9px; font-size: 13px; }
	.phone-hint { margin: -2px 0 2px; color: #858780; font-size: 10px; line-height: 1.5; }
	.direct-contacts {
		display: flex;
		flex-wrap: wrap;
		gap: 9px;
		margin-top: 7px;
	}
	.direct-contact {
		display: inline-flex;
		width: fit-content;
		align-items: center;
		gap: 10px;
		padding: 9px 12px;
		border-radius: 6px;
		color: #46564b;
		background: rgba(101, 118, 106, .07);
		transition: color .22s ease, background .22s ease, transform .22s ease;
	}
	.direct-contact:hover { color: #35433a; background: rgba(101, 118, 106, .13); transform: translateY(-1px); }
	.direct-contact svg { width: 23px; height: 23px; flex: 0 0 auto; }
	.whatsapp-contact svg { width: 23px; height: 23px; flex: 0 0 auto; fill: none; stroke: #25d366; stroke-linecap: round; stroke-linejoin: round; stroke-width: 1.5; }
	.whatsapp-contact svg path:last-child { fill: #25d366; stroke: none; }
	.direct-contact strong { font-size: 11px; font-weight: 700; letter-spacing: .005em; white-space: nowrap; }
	.gmail-contact svg { fill: none; stroke-linecap: round; stroke-linejoin: round; stroke-width: 2; }
	.gmail-contact .gmail-blue { stroke: #4285f4; }
	.gmail-contact .gmail-red { stroke: #ea4335; }
	.gmail-contact .gmail-green { stroke: #34a853; }
	.gmail-contact .gmail-gold { stroke: #fbbc04; }
	.connect-privacy { margin: 8px 0 0; color: #858780; font-size: 10px; line-height: 1.55; }
	.connect-error { margin: 5px 0 0; color: #9a4f3e; font-size: 12px; line-height: 1.5; }
	.connect-form .button { width: fit-content; margin-top: 18px; cursor: pointer; }
	.connect-form .button:disabled { cursor: wait; opacity: .65; transform: none; }
	.connect-confirmation .button { cursor: pointer; }
	@keyframes modal-backdrop-in { from { opacity: 0; } }
	@keyframes modal-content-in { from { opacity: 0; transform: translateY(12px); } }

	footer { background: var(--warm-beige); }
	@media (max-width: 900px) {
		.hero, .hero-minimal { min-height: 740px; }
		.hero-minimal { padding-top: 135px; padding-bottom: 84px; }
		.hero-illustrations { inset: 112px -10% 20px; }
		.hero-illustration { width: 100%; max-width: none; }
		.about-card, .about-card:first-child, .about-card:last-child { grid-template-columns: 1fr; gap: 28px; }
		.events-feature { grid-template-columns: 1fr; }
		.event-calendar { max-width: 600px; }
		.moments-gallery { grid-template-rows: 280px 280px; }
	}
	@media (max-width: 620px) {
		.header-actions { gap: 14px; }
		.language-toggle { gap: 4px; }
		.hero, .hero-minimal { min-height: 700px; }
		.hero-minimal { align-items: center; padding: 124px 24px 72px; }
		.hero h1 { font-size: clamp(72px, 24vw, 102px); }
		.hero-content { width: 100%; max-width: 420px; }
		.hero-statement { font-size: 30px; }
		.hero-tagline { max-width: 340px; }
		.hero-illustrations {
			top: 98px;
			right: 8px;
			bottom: 20px;
			left: 8px;
			height: auto;
			aspect-ratio: auto;
		}
		.hero-illustration { --hero-art-opacity: .56; width: 100%; height: 100%; object-fit: contain; }
		.illustration-space-needle,
		.illustration-board-game,
		.illustration-water-taxi,
		.illustration-hiking { display: none; }
		.hero-illustration-mobile { display: block; clip-path: none; animation-delay: .72s; }
		.about { padding-top: 100px; }
		.community-photo-break { width: calc(100% - 24px); height: 62vh; border-radius: 7px; }
		.community-photo-break p { right: 8%; bottom: 7%; left: 8%; text-align: left; }
		.events { padding-top: 100px; padding-bottom: 100px; }
		.events-heading { margin-bottom: 58px; }
		.events-feature { gap: 48px; }
		.calendar-heading { align-items: flex-start; flex-direction: column; gap: 8px; }
		.calendar-dates > span, .calendar-dates > button { width: 38px; height: 38px; }
		.moments-heading { margin-top: 100px; }
		.moments-gallery {
			display: flex;
			width: 100%;
			flex-direction: column;
			gap: 24px;
		}
		.moments-gallery > .moment,
		.moments-gallery > .moment-wide,
		.moments-gallery > .moment-tall,
		.moments-gallery > .moment-small,
		.moments-gallery > .moment-small:last-child {
			display: block;
			width: 100%;
			height: auto;
			flex: 0 0 auto;
			grid-column: auto;
			grid-row: auto;
			overflow: hidden;
			background: var(--warm-surface);
		}
		.moment > img { display: block; width: 100%; height: auto; object-fit: contain; transform: none; }
		.moment-tall img { object-position: center; }
		.hiking-slide { aspect-ratio: 4 / 3; background: #dfded6; }
		.hiking-slide img { width: 100%; height: 100%; object-fit: contain; transform: none; }
		.moment:hover img { transform: none; }
		.moment figcaption {
			position: static;
			align-items: flex-start;
			flex-direction: column;
			gap: 4px;
			padding: 18px 20px 20px;
			color: #414a43;
			background: var(--warm-surface);
		}
		.moment figcaption strong { font-size: 21px; }
		.moment figcaption span { color: #81766d; }
		.moment-wide .slide-arrow { top: calc((100vw - 48px) * .375); }
		.slide-previous { left: 12px; }
		.slide-next { right: 12px; }
		.slide-dots { top: calc((100vw - 48px) * .75 - 28px); right: 18px; bottom: auto; }
		.cta-actions { align-items: stretch; flex-direction: column; }
		.connect-modal-backdrop { padding: 14px; }
		.connect-modal { padding: 48px 24px 30px; }
		.connect-form .button, .connect-confirmation .button { width: 100%; }
	}
	@media (max-width: 700px) {
		.programs.section-wrap { padding: 82px 20px 92px; }
		.journey-section-heading h2 { font-size: clamp(42px, 13vw, 56px); }
		.program-grid.minimal.support-journey { gap: 22px; margin-top: 38px; }
		.program-grid.minimal.support-journey > .support-stop,
		.support-stop,
		.support-stop:nth-child(2),
		.support-stop:nth-child(3),
		.support-stop:nth-child(4) { padding: 0; overflow: hidden; }
		.support-stop .support-visual,
		.support-stop:nth-child(even) .support-visual {
			width: 100%;
			height: auto;
			aspect-ratio: 16 / 9;
			background: rgba(245, 240, 231, .78);
		}
		.support-stop .support-visual img,
		.support-stop:nth-child(even) .support-visual img {
			width: 100%;
			height: 100%;
			object-fit: contain;
			object-position: center;
			opacity: .9;
			transform: none;
		}
		.support-stop:hover .support-visual img { transform: none; }
		.support-stop .support-copy,
		.support-stop:nth-child(even) .support-copy {
			width: 100%;
			max-width: none;
			padding: 24px 22px 26px;
			border-radius: 0;
			background: var(--warm-surface);
			backdrop-filter: none;
		}
		.support-copy h3 { font-size: clamp(29px, 9vw, 36px); }
		.support-copy > p { font-size: 14px; }
		.support-activities { gap: 8px; }
		.support-activities li { padding: 8px 12px; font-size: 12px; }
	}
	@media (prefers-reduced-motion: reduce) {
		.hero-content > *, .hero-illustration { opacity: 1; animation: none; mask-size: 100% 100%; }
		.connect-modal-backdrop, .connect-modal, .hiking-slide img { animation: none; }
	}
</style>
