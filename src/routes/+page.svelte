<script lang="ts">
	import { onMount } from 'svelte';
	import { base } from '$app/paths';

	const programs = [
		{
			number: '01',
			title: 'Plan your path',
			color: 'sage'
		},
		{
			number: '02',
			title: 'Prepare to go',
			color: 'sand'
		},
		{
			number: '03',
			title: 'Belong & thrive',
			color: 'coral'
		}
	];

	const stories = [
		{
			quote:
				'My mentor helped me turn a confusing process into a clear plan. I arrived feeling prepared—not alone.',
			name: 'Nadia Rahman',
			detail: 'Bangladesh → Canada',
			image:
				'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'Kawan connected me with students who understood exactly what I was going through.',
			name: 'Mateo Silva',
			detail: 'Brazil → Germany',
			image:
				'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'I found a scholarship I would never have discovered on my own. It changed what felt possible.',
			name: 'Amara Okafor',
			detail: 'Nigeria → United Kingdom',
			image:
				'https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=240&q=85'
		}
	];

	let menuOpen = false;
	let storyIndex = 0;
	let email = '';
	let submitted = false;

	function subscribe() {
		if (email.trim()) {
			submitted = true;
			email = '';
		}
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) entry.target.classList.add('visible');
				}
			},
			{ threshold: 0.12 }
		);

		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>Kawan — Your journey. Our guidance.</title>
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label="Kawan home">
		<span>KAWAN</span><small>SEATTLE</small>
	</a>

	<nav class:open={menuOpen} aria-label="Primary navigation">
		<a href="#about" onclick={() => (menuOpen = false)}>About</a>
		<a href="#programs" onclick={() => (menuOpen = false)}>How we help</a>
		<a href="#stories" onclick={() => (menuOpen = false)}>Stories</a>
	</nav>

	<a class="desktop-cta" href="#connect">Connect</a>
	<button
		class="menu-button"
		class:active={menuOpen}
		aria-label="Toggle navigation"
		aria-expanded={menuOpen}
		onclick={() => (menuOpen = !menuOpen)}
	>
		<span></span><span></span>
	</button>
</header>

<main id="top">
	<section class="hero">
		<div class="hero-minimal">
			<div class="hero-content reveal visible">
				<h1><span class="welcome-to-text">welcome to</span><br /><span class="kawan-script">kawan</span></h1>
				<p class="hero-tagline">guidance for international students in seattle</p>
				<div class="hero-actions">
					<a class="button" href="#programs">let's start</a>
				</div>
			</div>
			<div class="hero-shape"></div>
			<img class="seattle-art" src={`${base}/images/seattle-skyline-subtle.png`} alt="" aria-hidden="true" />
		</div>
	</section>

	<section class="about section-wrap" id="about">
		<div class="about-intro reveal">
			<p class="about-eyebrow">about us</p>
			<h2>A friend for the journey.</h2>
			<p class="journey-prologue">From the first unfamiliar arrival to the moment Seattle begins to feel like home, Kawan walks beside you.</p>
		</div>
		<div class="illustration-band reveal" id="our-story">
			<div class="illustration-copy">
				<span class="hand-note">01 · Our Story</span>
				<p class="story-lead"><strong>KAWAN means “friend” or “companion” in Indonesian.</strong> We chose it because starting life in a new country is easier with people beside you.</p>
				<p>Founded by international students, we understand the questions that come with moving to the U.S.—from housing and school to friendships and careers.</p>
				<p>Through practical resources, events, and community, we help international students feel supported, connected, and ready to thrive.</p>
			</div>
			<figure class="about-photo-frame">
				<div class="about-photo-crop">
					<img src={`${base}/images/kawan-community-christmas-2025.jpeg`} alt="KAWAN community members gathering at Evergreen Christmas Lights in 2025" />
				</div>
			</figure>
			<img class="story-watercolor" src={`${base}/images/watercolor-neighborhood.png`} alt="Watercolor of a leafy Seattle neighborhood with apartments and the Space Needle" />
		</div>
		<div class="belief-heading reveal">
			<p class="about-eyebrow">our direction</p>
			<h2>What guides us.</h2>
		</div>
		<div class="about-grid reveal">
			<article class="about-card" id="our-vision">
				<div class="belief-label"><span>01</span><p class="about-label">our vision</p></div>
				<div class="belief-copy">
					<h3>Make belonging feel possible.</h3>
					<p class="about-description">We imagine a Seattle where international students feel welcomed, understood, and part of the community from day one.</p>
				</div>
			</article>
			<article class="about-card" id="our-mission">
				<div class="belief-label"><span>02</span><p class="about-label">our mission</p></div>
				<div class="belief-copy">
					<h3>Build connection, confidence, and care.</h3>
					<p class="about-description">Through mentoring, friendship, and practical guidance, we help students settle in, thrive, and feel at home.</p>
				</div>
			</article>
		</div>
	</section>

	<section class="programs section-wrap" id="programs">
		<div class="journey-section-heading reveal">
			<p class="about-eyebrow">How we help</p>
			<h2>Little by little, life becomes familiar.</h2>
			<p>Practical milestones become moments of confidence—with someone nearby whenever you need a hand.</p>
		</div>
		<figure class="section-watercolor help-watercolor reveal">
			<img src={`${base}/images/watercolor-student-life.png`} alt="Watercolor of a Seattle campus, café, notebook, and everyday student essentials" />
		</figure>
		<div class="program-grid minimal">
			{#each programs as program, index}
				<article class="program-card {program.color} reveal" style={`--delay: ${index * 90}ms`}>
					<div class="card-icon">
						{#if index === 0}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<circle cx="20" cy="20" r="14" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{:else if index === 1}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<rect x="10" y="10" width="20" height="20" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{:else}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<path d="M20 31s-11-5.8-11-13.3A6.7 6.7 0 0 1 20 12.5a6.7 6.7 0 0 1 11 5.2C31 25.2 20 31 20 31Z" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{/if}
					</div>
					<h3>{program.title}</h3>
					<a href="#connect" aria-label={`Explore ${program.title}`}>Learn more <span>↗</span></a>
				</article>
			{/each}
		</div>
	</section>

	<section class="mentor-section" id="connect">
		<div class="section-wrap">
			<div class="mentor-minimal reveal">
				<div class="mentor-copy">
					<p class="about-eyebrow">Get involved</p>
					<h2>There’s a place for you here.</h2>
					<p>Meet a mentor, share what you know, or help welcome the next student finding their footing in Seattle.</p>
					<div class="involve-actions"><a class="button gold" href="mailto:hello@kawan.org">Find a mentor <span>↗</span></a><a class="text-link" href="mailto:volunteer@kawan.org">Volunteer with us</a></div>
				</div>
				<figure class="section-watercolor community-watercolor">
					<img src={`${base}/images/watercolor-community.png`} alt="Watercolor of international students gathering around a café table in Seattle" />
				</figure>
			</div>
		</div>
	</section>

	<section class="stories section-wrap" id="stories">
		<div class="journey-section-heading stories-heading reveal">
			<p class="about-eyebrow">belonging</p>
			<h2>The journey becomes a shared one.</h2>
		</div>
		<div class="story-card reveal">
			<div class="quote-mark">"</div>
			<blockquote>{stories[storyIndex].quote}</blockquote>
			<div class="student">
				<img src={stories[storyIndex].image} alt={stories[storyIndex].name} />
				<div><strong>{stories[storyIndex].name}</strong><span>{stories[storyIndex].detail}</span></div>
			</div>
			<div class="story-progress">
				{#each stories as _, index}
					<button class:active={index === storyIndex} onclick={() => (storyIndex = index)} aria-label={`Show story ${index + 1}`}></button>
				{/each}
			</div>
		</div>
	</section>

	<section class="cta-minimal">
		<div class="section-wrap">
			<div class="cta-content reveal">
				<p class="about-eyebrow">your next chapter</p>
				<h2>Find your way home.</h2>
				<a class="button gold large" href="mailto:hello@kawan.org">Get started <span>↗</span></a>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="footer-main section-wrap">
		<div class="footer-brand">
			<a class="brand inverse" href="#top">
				<span class="brand-mark" aria-hidden="true">
					<svg viewBox="0 0 44 44" fill="none">
						<path d="M5 27.5c7-12 16-15 33-12-7.5 2.8-11 8-12.2 15.2C20 24.8 13.2 24.5 5 27.5Z" fill="currentColor" />
						<path d="M10 32c8-5 15-5.8 24-3.2" stroke="currentColor" stroke-width="2.7" stroke-linecap="round" />
					</svg>
				</span>
				<span>Kawan</span>
			</a>
			<p>Guidance without borders.</p>
		</div>
		<div class="footer-links">
			<div><strong>LINKS</strong><a href="#programs">How we help</a><a href="#stories">Stories</a></div>
			<div><strong>GET INVOLVED</strong><a href="mailto:volunteer@kawan.org">Volunteer</a><a href="mailto:hello@kawan.org">Contact us</a></div>
		</div>
	</div>
	<div class="footer-bottom section-wrap">
		<span>© 2026 KAWAN.</span>
	</div>
</footer>

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

	.brand-mark {
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

	.button.small {
		min-height: 42px;
		padding: 0 17px;
	}

	.button.large {
		min-height: 60px;
		padding: 0 32px;
		font-size: 16px;
	}

	.button.gold {
		color: var(--ink);
		background: var(--gold);
		box-shadow: none;
	}

	.button.gold:hover {
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

	.welcome-to-text {
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
	.hero-shape {
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

	.about-intro {
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

	.card-icon svg {
		width: 100%;
		height: 100%;
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

	.program-card a {
		color: var(--ink);
		font-size: 14px;
		font-weight: 700;
		text-decoration: none;
		display: inline-flex;
		align-items: center;
		gap: 8px;
		border-bottom: 1px solid var(--ink);
		padding-bottom: 5px;
		width: fit-content;
	}

	/* Mentor Section */
	.mentor-section {
		padding: 120px 0;
		background: #ede4db;
	}

	.mentor-minimal {
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}

	.mentor-dot {
		width: 80px;
		height: 80px;
		border: 2px solid var(--forest);
		border-radius: 50%;
		margin: 0 auto 40px;
	}

	.mentor-minimal h2 {
		font-size: 48px;
		margin: 0 0 16px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -1px;
	}

	.mentor-minimal p {
		color: var(--muted);
		font-size: 16px;
		margin: 0 0 32px 0;
		line-height: 1.6;
	}

	/* Stories Section */
	.stories {
		padding: 100px 0;
	}

	.story-card {
		max-width: 720px;
		margin: 0 auto;
		padding: 60px;
		background: linear-gradient(180deg, rgba(245,238,234,0.95), rgba(255,255,255,0.7));
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 24px;
		box-shadow: 0 22px 50px rgba(91, 74, 66, 0.04);
	}

	.quote-mark {
		font-size: 80px;
		color: var(--gold);
		line-height: 0.6;
		margin-bottom: 20px;
	}

	blockquote {
		margin: 0 0 40px 0;
		font-size: 24px;
		line-height: 1.6;
		color: var(--ink);
		font-style: italic;
	}

	.student {
		display: flex;
		align-items: center;
		gap: 16px;
		margin-bottom: 32px;
	}

	.student img {
		width: 60px;
		height: 60px;
		border-radius: 50%;
	}

	.student strong {
		display: block;
		color: var(--ink);
	}

	.student span {
		display: block;
		font-size: 13px;
		color: var(--muted);
	}

	.story-progress {
		display: flex;
		gap: 8px;
		justify-content: center;
	}

	.story-progress button {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: rgba(91, 74, 66, 0.2);
		border: none;
		cursor: pointer;
		transition: background 0.3s ease;
	}

	.story-progress button.active {
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

		.hero-shape {
			display: none;
		}

		.about-content {
			grid-template-columns: 1fr;
			gap: 60px;
		}

		.about-content h3 {
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

		.story-card {
			padding: 40px;
		}

		.mentor-section {
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

	.welcome-to-text {
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

	.illustration-band img {
		position: relative;
		z-index: 1;
		width: 100%;
		filter: drop-shadow(0 18px 22px rgba(109, 92, 84, 0.08));
	}

	.about-photo-frame {
		position: relative;
		z-index: 1;
		margin: 0;
		padding: 10px 10px 15px;
		background: #fff;
		box-shadow: 0 18px 42px rgba(109, 92, 84, 0.12);
		transform: rotate(1.5deg);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}

	.about-photo-frame:hover {
		box-shadow: 0 22px 50px rgba(109, 92, 84, 0.16);
		transform: rotate(0deg) translateY(-3px);
	}

	.about-photo-crop {
		position: relative;
		aspect-ratio: 1.52;
		overflow: hidden;
		background: #eee7df;
	}

	.about-photo-crop img {
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

	.hand-note {
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

	.hand-note::before {
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
		.about-photo-frame { margin-top: 20px; }
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

	.brand small {
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
	.hero-shape,
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

	.about-photo-frame,
	.about-photo-frame:hover {
		padding: 8px 8px 14px;
		border-radius: 18px;
		box-shadow: 0 16px 38px rgba(109, 92, 84, 0.1);
		transform: none;
	}

	.about-photo-crop {
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
	.hero .welcome-to-text,
	.hero .kawan-script {
		font-family: 'Fraunces', serif;
	}

	.hero h1 {
		font-weight: 600;
		letter-spacing: -3px;
	}

	.hero .welcome-to-text {
		font-weight: 500;
		letter-spacing: -0.5px;
	}

	.hero .kawan-script {
		font-weight: 700;
		letter-spacing: -4px;
	}

	/* About story hierarchy */
	.about-intro {
		max-width: 760px;
		margin-bottom: 40px;
		text-align: center;
	}

	.about-intro h2,
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
		.about-intro { margin-bottom: 30px; }
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
	.seattle-art {
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
		.seattle-art {
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

	.about-intro,
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

	.belief-label span {
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

	.journey-thread {
		position: absolute;
		z-index: -1;
		inset: 78vh 0 0;
		pointer-events: none;
	}

	.journey-thread svg {
		display: block;
		width: 100%;
		height: 100%;
		overflow: visible;
	}

	.journey-thread path {
		fill: none;
		vector-effect: non-scaling-stroke;
	}

	.journey-wash {
		stroke: rgba(167, 180, 158, 0.12);
		stroke-width: 34;
		stroke-linecap: round;
	}

	.journey-line {
		stroke: rgba(160, 127, 105, 0.26);
		stroke-width: 1.5;
		stroke-dasharray: 2 8;
		stroke-linecap: round;
	}

	.about,
	.mentor-section,
	.cta-minimal {
		background: transparent;
	}

	.about,
	.programs,
	.mentor-section,
	.stories,
	.cta-minimal {
		position: relative;
		z-index: 1;
	}

	.journey-prologue {
		max-width: 620px;
		margin: 22px auto 0;
		color: var(--muted);
		font-family: 'Fraunces', serif;
		font-size: 19px;
		line-height: 1.65;
	}

	.journey-vignette {
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

	.journey-vignette-arrival {
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

	.journey-vignette-daily {
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

	.mentor-section {
		padding: 150px 0;
	}

	.mentor-minimal {
		padding: 70px 42px;
		border-top: 1px solid rgba(109, 92, 84, 0.14);
		border-bottom: 1px solid rgba(109, 92, 84, 0.14);
	}

	.mentor-dot {
		display: none;
	}

	.journey-marker {
		position: relative;
		width: 70px;
		height: 42px;
		margin: 0 auto 24px;
	}

	.journey-marker::before,
	.journey-marker::after,
	.journey-marker span {
		position: absolute;
		border-radius: 50% 50% 48% 52%;
		content: '';
	}

	.journey-marker::before {
		inset: 3px 8px 5px 5px;
		background: rgba(167, 180, 158, 0.2);
		transform: rotate(-8deg);
	}

	.journey-marker::after {
		inset: 9px 3px 2px 13px;
		border: 1px solid rgba(201, 134, 107, 0.5);
		transform: rotate(7deg);
	}

	.stories {
		padding-top: 110px;
		padding-bottom: 130px;
	}

	.stories-heading {
		margin-bottom: 54px;
	}

	.story-card {
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
		.journey-thread {
			top: 72vh;
			opacity: 0.65;
		}

		.journey-wash {
			stroke-width: 20;
		}

		.journey-vignette-arrival,
		.journey-vignette-daily {
			width: 150vw;
			margin-left: -35vw;
		}

		.journey-vignette-arrival {
			margin-top: -10px;
			margin-bottom: -70px;
		}

		.journey-vignette-daily {
			margin-top: -10px;
			margin-bottom: -80px;
		}

		:global(.journey-vignette figcaption) {
			bottom: 4%;
		}

		.programs,
		.mentor-section,
		.stories,
		.cta-minimal {
			padding-top: 90px;
			padding-bottom: 90px;
		}

		.journey-section-heading h2 {
			font-size: 42px;
		}

		.mentor-minimal {
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
	.seattle-art { position: absolute; z-index: 0; inset: 0; width: 100%; height: 100%; object-fit: cover; object-position: center; opacity: .96; }
	.hero-content { position: absolute; z-index: 2; top: 24%; left: max(36px, calc((100vw - 1280px) / 2)); max-width: 630px; text-align: left; }
	.hero-kicker { margin-bottom: 26px; font-family: Arial, sans-serif; font-size: 10px; font-weight: 700; letter-spacing: .2em; text-transform: uppercase; }
	h1 { margin-bottom: 28px; font-family: Georgia, 'Times New Roman', serif; font-size: clamp(66px, 7.4vw, 112px); font-weight: 400; line-height: .87; letter-spacing: -.055em; text-transform: none; }
	.welcome-to-text { font-size: 1em; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script { padding: 0; color: #526258; font-family: Georgia, 'Times New Roman', serif; font-size: 1em; font-style: italic; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script::before, .kawan-script::after { display: none; }
	.hero-tagline { max-width: 470px; margin-bottom: 30px; color: #505851; font-family: Arial, sans-serif; font-size: 15px; line-height: 1.75; text-transform: none; }
	.hero-actions { justify-content: flex-start; margin-top: 0; }
	.button, .button.gold { min-height: 48px; padding: 0 20px; border: 1px solid #3f4d45; border-radius: 0; color: #f8f4eb; background: #3f4d45; box-shadow: 5px 5px 0 rgba(63,77,69,.13); font-family: Arial, sans-serif; font-size: 11px; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; }
	.button:hover, .button.gold:hover { color: #f8f4eb; background: #2f3c35; box-shadow: 7px 7px 0 rgba(63,77,69,.12); }
	.hero-caption { position: absolute; z-index: 2; right: 4%; bottom: 5%; margin: 0; padding-left: 36px; color: #414a44; font-family: Arial, sans-serif; font-size: 10px; letter-spacing: .08em; }
	.hero-caption::before { position: absolute; top: 50%; left: 0; width: 24px; height: 1px; background: currentColor; content: ''; }
	.hero-caption span { margin-right: 10px; font-weight: 700; text-transform: uppercase; }

	.about, .programs, .stories, .cta-minimal, footer { background: #f4efe5; }
	.about, .programs, .stories { padding-top: 145px; padding-bottom: 145px; }
	.about::before, .about::after { display: none; }
	.about-intro, .journey-section-heading { text-align: left; margin-left: 0; }
	.about-intro h2, .journey-section-heading h2, .mentor-minimal h2, .cta-content h2 { font-family: Georgia, 'Times New Roman', serif; font-weight: 400; letter-spacing: -.045em; }
	.about-eyebrow { color: #7b6251; font-family: Arial, sans-serif; font-size: 9px; letter-spacing: .22em; }
	.journey-vignette img, .about-photo-crop { border-radius: 0; filter: saturate(.72) sepia(.08); }
	.about-photo-frame { transform: rotate(1.5deg); }
	.about-grid { grid-template-columns: 1fr 1fr; gap: 0; border-top: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); }
	.about-card { min-height: 0; padding: 42px; border: 0; border-radius: 0; background: transparent; box-shadow: none; }
	.about-card + .about-card { border-left: 1px solid rgba(52,58,53,.22); }
	.about-card:hover, .program-card:hover { transform: none; box-shadow: none; }
	.program-grid.minimal { gap: 0; border-top: 1px solid rgba(52,58,53,.22); }
	.program-card { min-height: 310px; padding: 42px 34px; border: 0; border-right: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	.card-icon { width: 34px; height: 34px; opacity: .62; }
	.program-card h3 { margin-top: auto; font-family: Georgia, 'Times New Roman', serif; font-size: 32px; font-weight: 400; }
	.mentor-section { background: #d9d3c4; }
	.mentor-minimal { border-color: rgba(52,58,53,.3); }
	.story-card { border: 0; border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	blockquote { font-family: Georgia, 'Times New Roman', serif; font-size: clamp(26px, 3vw, 40px); line-height: 1.42; }
	.student img { filter: grayscale(.35) sepia(.15); }
	.cta-minimal { border-top: 1px solid rgba(52,58,53,.18); }
	footer { border-top: 1px solid rgba(52,58,53,.22); }

	@media (max-width: 768px) {
		.site-header { width: calc(100% - 36px); height: 72px; }
		.desktop-cta { display: none; }
		nav.open { position: absolute; top: 72px; left: 0; display: flex; width: 100%; padding: 28px; flex-direction: column; gap: 24px; background: #f4efe5; border-bottom: 1px solid rgba(52,58,53,.2); }
		.menu-button { border-radius: 0; background: #3f4d45; }
		.hero-minimal { height: 820px; min-height: 820px; }
		.seattle-art { object-position: 62% center; opacity: .58; }
		.hero-content { top: 20%; right: 24px; left: 24px; }
		h1 { font-size: clamp(56px, 18vw, 82px); }
		.hero-tagline { max-width: 360px; }
		.hero-caption { right: 24px; bottom: 26px; }
		.about, .programs, .stories { padding-top: 90px; padding-bottom: 90px; }
		.about-grid { grid-template-columns: 1fr; }
		.about-card + .about-card { border-top: 1px solid rgba(52,58,53,.22); border-left: 0; }
		.program-card { min-height: 220px; border-left: 1px solid rgba(52,58,53,.22); }
		.story-card { padding: 20px 0; }
	}
	*/

	/* Cohesive watercolor section system — cover intentionally unchanged */
	:global(main) {
		background: #fbf8f2;
	}

	.about,
	.programs,
	.mentor-section,
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

	.about-intro,
	.belief-heading,
	.journey-section-heading {
		max-width: 720px;
		margin-right: auto;
		margin-left: auto;
		text-align: center;
	}

	.about-eyebrow,
	.hand-note {
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

	.about-photo-frame,
	.about-photo-frame:hover {
		z-index: 2;
		margin: 0;
		padding: 9px 9px 22px;
		border-radius: 1px;
		background: #fffdf8;
		box-shadow: 0 24px 54px rgba(72, 62, 52, 0.14);
		transform: rotate(1.2deg);
	}

	.about-photo-crop { border-radius: 0; }

	.story-watercolor {
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
	.section-watercolor { margin: 0; pointer-events: none; }
	.help-watercolor {
		width: min(860px, 78vw);
		margin: -10px auto -150px;
		opacity: 0.58;
	}
	.section-watercolor img { width: 100%; filter: saturate(0.58); }
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

	.mentor-section {
		overflow: hidden;
		padding: 150px 0 130px;
		background: #f6f1e7;
	}
	.mentor-minimal {
		display: grid;
		max-width: 1180px;
		grid-template-columns: 0.75fr 1.25fr;
		gap: 64px;
		align-items: center;
		padding: 60px 0;
		border-color: rgba(109, 92, 84, 0.16);
		text-align: left;
	}
	.mentor-copy { position: relative; z-index: 2; }
	.mentor-minimal h2 { margin-top: 10px; font-family: 'Fraunces', serif; font-size: clamp(46px, 5vw, 70px); line-height: 1; }
	.mentor-minimal p { max-width: 470px; font-size: 16px; line-height: 1.75; }
	.community-watercolor { margin: -80px -16% -90px -5%; opacity: 0.72; }
	.involve-actions { display: flex; align-items: center; gap: 28px; }
	.text-link { padding-bottom: 5px; border-bottom: 1px solid #78685e; color: #514843; font-size: 13px; font-weight: 650; }

	.stories { padding-top: 140px; padding-bottom: 140px; background: #fbf8f2; }
	.story-card { max-width: 820px; border-radius: 2px; background: #fffdf8; box-shadow: 0 24px 60px rgba(76, 70, 59, 0.07); }
	.cta-minimal { background: #e4e9df; }

	@media (max-width: 768px) {
		.about { padding-top: 92px; }
		.illustration-band { min-height: 0; grid-template-columns: 1fr; gap: 36px; margin: 44px 0 105px; padding: 38px 24px 100px; }
		.story-watercolor { right: -28%; bottom: -15%; width: 100% !important; opacity: .55; }
		.about-card, .about-card:first-child { grid-template-columns: 1fr; padding: 42px 4px; }
		.programs { padding-top: 105px; padding-bottom: 100px; }
		.help-watercolor { width: 135vw; margin: -10px 0 -70px -28vw; }
		.program-grid.minimal { margin-top: 70px; }
		.mentor-section { padding: 90px 0; }
		.mentor-minimal { grid-template-columns: 1fr; gap: 20px; padding: 30px 0; }
		.community-watercolor { width: 130%; margin: -20px -15% -35px; opacity: .62; }
		.involve-actions { align-items: flex-start; flex-direction: column; gap: 20px; }
		.stories { padding-top: 90px; padding-bottom: 90px; }
	}
</style>
