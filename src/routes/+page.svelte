<script lang="ts">
	import { onMount } from 'svelte';

	let menuOpen = false;

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => entries.forEach((entry) => entry.isIntersecting && entry.target.classList.add('visible')),
			{ threshold: 0.12 }
		);
		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>KAWAN Seattle — Find your people. Feel at home.</title>
	<meta name="description" content="KAWAN welcomes international students to Seattle with practical support, friendship, mentorship, and community." />
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label="KAWAN Seattle home">
		<span class="brand-mark" aria-hidden="true">K</span>
		<span>KAWAN <small>SEATTLE</small></span>
	</a>
	<nav class:open={menuOpen} aria-label="Main navigation">
		<details class="nav-dropdown">
			<summary>About us <span aria-hidden="true">⌄</span></summary>
			<div class="dropdown-menu">
				<a href="#about" onclick={() => (menuOpen = false)}>Our story</a>
				<a href="#vision" onclick={() => (menuOpen = false)}>Our vision &amp; mission</a>
			</div>
		</details>
		<a href="#support" onclick={() => (menuOpen = false)}>How we help</a>
		<a href="#community" onclick={() => (menuOpen = false)}>Community</a>
	</nav>
	<a class="button header-cta" href="mailto:hello@kawanseattle.org">Connect with us <span>↗</span></a>
	<button class="menu" aria-label="Toggle menu" aria-expanded={menuOpen} onclick={() => (menuOpen = !menuOpen)}>
		<span></span><span></span>
	</button>
</header>

<main id="top">
	<section class="hero">
		<div class="hero-copy reveal visible">
			<p class="eyebrow"><span></span> Welcome to Seattle</p>
			<h1>Welcome to <em>KAWAN.</em></h1>
			<p class="lead"><em>Built by international students, for international students.</em></p>
			<div class="actions">
				<a class="button" href="mailto:hello@kawanseattle.org">Join the community <span>↗</span></a>
				<a class="text-link" href="#support">See how we help <span>↓</span></a>
			</div>
		</div>
	</section>

	<section class="intro" id="about">
		<div class="section-wrap intro-grid">
			<div class="reveal">
				<p class="eyebrow light"><span></span> Our name, our promise</p>
				<h2>KAWAN means <em>friend.</em></h2>
			</div>
			<div class="intro-copy reveal">
				<p>Moving to a new country is easier when you have people to go through it with.</p>
				<p>We're international students who have been through the same journey, and we want to help you navigate yours.</p>
			</div>
		</div>
	</section>

	<section class="vision section-wrap" id="vision">
		<div class="vision-heading reveal">
			<p class="eyebrow"><span></span> Our direction</p>
			<h2>Why we’re here.</h2>
		</div>
		<div class="vision-grid">
			<article class="reveal">
				<small>OUR VISION</small>
				<h3>International students equipped to thrive.</h3>
				<p>We envision students growing with confidence during college and carrying that foundation into the years ahead.</p>
			</article>
			<article class="reveal">
				<small>OUR MISSION</small>
				<h3>Practical support. Meaningful connection.</h3>
				<p>We help with everyday needs, academic and career resources, mentorship, and a community where students belong.</p>
			</article>
		</div>
	</section>

	<section class="support section-wrap" id="support">
		<div class="section-heading reveal">
			<p class="eyebrow"><span></span> Here for the real stuff</p>
			<h2>Support for life<br /><em>beyond the classroom.</em></h2>
		</div>
		<div class="support-grid">
			<article class="support-card life reveal">
				<div class="card-icon">⌂</div><span>01</span>
				<h3>Settle into life</h3>
				<p>Get help navigating housing, phones, banking, and everyday life in the U.S.</p>
			</article>
			<article class="support-card grow reveal">
				<div class="card-icon">↗</div><span>02</span>
				<h3>Grow with guidance</h3>
				<p>Connect with mentorship, academic resources, and practical career preparation.</p>
			</article>
			<article class="support-card belong reveal">
				<div class="card-icon">☺</div><span>03</span>
				<h3>Build your circle</h3>
				<p>Meet friends, join local events, and become part of a caring community.</p>
			</article>
		</div>
	</section>

	<section class="community" id="community">
		<div class="community-photo reveal">
			<img src="https://images.unsplash.com/photo-1517486808906-6ca8b3f04846?auto=format&fit=crop&w=1300&q=85" alt="A diverse group of students enjoying time together" />
			<div class="photo-note">Come as you are ✦</div>
		</div>
		<div class="community-copy reveal">
			<p class="eyebrow light"><span></span> More than a network</p>
			<h2>A place to<br /><em>belong.</em></h2>
			<p>Studying abroad is about more than earning a degree. It’s about finding connection, discovering opportunities, and building a future with people beside you.</p>
			<a class="button gold" href="mailto:hello@kawanseattle.org">Say hello <span>↗</span></a>
		</div>
	</section>

	<section class="final-cta">
		<div class="cta-inner reveal">
			<p class="eyebrow centered"><span></span> Your Seattle chapter starts here <span></span></p>
			<h2>New city. New chapter.<br /><em>New friends.</em></h2>
			<p>Whether you just arrived or have been here a while, there’s a place for you at KAWAN.</p>
			<div class="actions centered-actions">
				<a class="button gold" href="mailto:hello@kawanseattle.org">Connect with KAWAN <span>↗</span></a>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="section-wrap footer-row">
		<a class="brand inverse" href="#top"><span class="brand-mark">K</span><span>KAWAN <small>SEATTLE</small></span></a>
		<p>Friendship, support, and community<br />for international students.</p>
		<div class="footer-links"><a href="#about">About</a><a href="#support">Support</a><a href="mailto:hello@kawanseattle.org">Contact</a></div>
	</div>
	<div class="section-wrap footer-bottom"><span>© 2026 KAWAN Seattle</span><span>Built with care in Seattle, WA</span></div>
</footer>

<style>
	:global(.reveal){opacity:0;transform:translateY(22px);transition:opacity .7s ease,transform .7s ease}.reveal.visible{opacity:1;transform:none}
	.site-header{position:absolute;z-index:20;top:0;left:50%;display:flex;width:min(1240px,calc(100% - 64px));height:96px;align-items:center;justify-content:space-between;transform:translateX(-50%)}
	.brand{display:flex;align-items:center;gap:10px;font:800 20px/1 'Manrope',sans-serif;letter-spacing:-.5px}.brand small{display:block;margin-top:4px;color:var(--forest);font-size:8px;letter-spacing:2.6px}.brand-mark{display:grid;width:42px;height:42px;place-items:center;border-radius:50% 50% 46% 54%;color:white;background:var(--forest);font-size:20px}.brand.inverse small{color:var(--gold)}
	nav{display:flex;gap:36px;margin-left:80px}nav a{font-size:14px;font-weight:600}.button{display:inline-flex;min-height:52px;align-items:center;justify-content:center;gap:18px;padding:0 25px;border-radius:7px;color:white;background:var(--forest);box-shadow:0 10px 25px #145f522a;font-size:14px;font-weight:700;transition:.2s}.button:hover{background:var(--forest-dark);transform:translateY(-2px)}.button.gold{color:var(--ink);background:var(--gold);box-shadow:none}.header-cta{min-height:44px}.menu{display:none}
	.hero{position:relative;display:grid;min-height:780px;grid-template-columns:minmax(340px,540px) minmax(460px,620px);align-items:center;justify-content:center;gap:58px;overflow:hidden;padding:115px 52px 50px;background:linear-gradient(105deg,#f9f4e8 0 56%,#dceee7 56%)}.hero:before{position:absolute;top:-210px;left:-140px;width:520px;height:520px;border:1px solid #145f5218;border-radius:50%;content:''}.hero-copy{position:relative;z-index:2}.eyebrow{display:flex;align-items:center;gap:10px;margin-bottom:22px;color:var(--forest);font-size:11px;font-weight:800;letter-spacing:2px;text-transform:uppercase}.eyebrow span{width:26px;height:2px;background:var(--gold)}.eyebrow.light{color:#dcefe8}.hero h1,.section-heading h2,.intro h2,.community h2,.final-cta h2{margin:0;font:700 clamp(48px,5.4vw,76px)/1.03 'Manrope',sans-serif;letter-spacing:-4px}.hero h1 em,h2 em{color:var(--forest);font-family:Georgia,serif;font-weight:400}.lead{max-width:500px;margin:30px 0;color:#4f6862;font-size:19px;line-height:1.65}.actions{display:flex;align-items:center;gap:27px}.text-link,.volunteer-link{border-bottom:1px solid #9faaa7;padding:10px 0;font-size:14px;font-weight:700}
	.hero-art{position:relative;height:540px}.photo-main{position:absolute;top:25px;right:0;width:79%;height:440px;overflow:hidden;border-radius:180px 180px 20px 20px;box-shadow:0 30px 60px #194e4230}.photo-main img,.photo-small img,.community-photo img{width:100%;height:100%;object-fit:cover}.photo-main img{object-position:center}.photo-small{position:absolute;bottom:0;left:0;width:190px;height:215px;overflow:hidden;border:9px solid #dceee7;border-radius:100px 100px 12px 12px}.hello-card{position:absolute;top:0;left:3%;display:flex;width:150px;height:150px;flex-direction:column;align-items:center;justify-content:center;border-radius:50%;color:var(--ink);background:var(--gold);box-shadow:0 15px 35px #8b67262e;transform:rotate(-8deg)}.hello-card span{font:italic 28px Georgia}.hello-card strong{margin-top:5px;font-size:12px}.hello-card small{margin-top:4px;font-size:8px;letter-spacing:2px}.doodle{position:absolute;right:-18px;bottom:12px;width:150px;color:var(--forest)}.location-pill{position:absolute;right:8%;bottom:28px;padding:11px 16px;border-radius:100px;background:#fff;font-size:11px;font-weight:700;letter-spacing:1px}
	.section-wrap{width:min(1160px,calc(100% - 64px));margin:auto}.intro{padding:110px 0;color:white;background:var(--forest)}.intro-grid{display:grid;grid-template-columns:1fr 1fr;gap:100px}.intro h2{font-size:clamp(45px,5vw,68px)}.intro h2 em{color:var(--gold)}.intro-copy{padding-top:8px}.intro-copy p{max-width:530px;margin-bottom:22px;font-size:18px;line-height:1.75}.intro-copy p:first-child{font-weight:700}
	.support{padding:120px 0}.section-heading{text-align:center}.section-heading .eyebrow{justify-content:center}.section-heading h2{font-size:clamp(44px,5vw,66px)}.support-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;margin-top:62px}.support-card{position:relative;min-height:340px;padding:35px;border-radius:14px}.support-card.life{background:#e1efe9}.support-card.grow{background:#f5ead6}.support-card.belong{background:#f2d3c8}.support-card>span{position:absolute;top:35px;right:35px;font-size:11px;font-weight:800}.card-icon{display:grid;width:65px;height:65px;place-items:center;border:1px solid #18352f55;border-radius:50%;font:28px Georgia}.support-card h3{margin:70px 0 14px;font-size:25px;letter-spacing:-1px}.support-card p{color:#536963;line-height:1.7}
	.community{display:grid;grid-template-columns:1.12fr .88fr;min-height:650px;background:#123f37}.community-photo{position:relative;min-height:650px}.community-photo img{object-position:center}.photo-note{position:absolute;right:30px;bottom:28px;padding:14px 18px;border-radius:7px;background:#fff;font-family:Georgia,serif;font-style:italic}.community-copy{display:flex;max-width:520px;flex-direction:column;align-items:flex-start;justify-content:center;padding:70px;color:#fff}.community-copy h2{font-size:clamp(50px,5vw,72px)}.community-copy h2 em{color:var(--gold)}.community-copy>p:not(.eyebrow){margin:28px 0 32px;color:#d5e4df;font-size:17px;line-height:1.75}
	.final-cta{position:relative;overflow:hidden;padding:125px 30px;text-align:center;background:#e7f2ee}.final-cta:before,.final-cta:after{position:absolute;width:400px;height:400px;border:1px solid #145f521a;border-radius:50%;content:''}.final-cta:before{top:-240px;left:-80px}.final-cta:after{right:-100px;bottom:-280px}.cta-inner{position:relative;z-index:1}.eyebrow.centered{justify-content:center}.final-cta h2{font-size:clamp(46px,5.5vw,72px)}.final-cta>div>p:not(.eyebrow){max-width:560px;margin:25px auto 33px;color:var(--muted);font-size:17px;line-height:1.6}.centered-actions{justify-content:center}
	footer{padding:70px 0 25px;color:#fff;background:#0d302a}.footer-row{display:grid;grid-template-columns:1fr 1fr 1fr;align-items:start}.footer-row p{color:#b9cdc7;line-height:1.6}.footer-links{display:flex;justify-content:flex-end;gap:25px;font-size:14px}.footer-bottom{display:flex;justify-content:space-between;margin-top:55px;padding-top:22px;border-top:1px solid #ffffff1f;color:#8fa8a1;font-size:11px;letter-spacing:1px;text-transform:uppercase}
	@media(max-width:800px){.site-header{width:calc(100% - 36px);height:78px}.header-cta{display:none}.menu{display:block;width:43px;height:43px;padding:12px;border-radius:50%;background:var(--forest)}.menu span{display:block;height:2px;margin:5px 0;background:#fff}nav{position:absolute;top:68px;right:0;display:none;width:210px;flex-direction:column;gap:0;margin:0;padding:12px;border-radius:10px;background:#fff;box-shadow:var(--shadow)}nav.open{display:flex}nav a{padding:13px}.hero{min-height:auto;grid-template-columns:1fr;gap:25px;padding:125px 24px 70px;background:linear-gradient(160deg,#f9f4e8 0 58%,#dceee7 58%)}.hero h1{font-size:49px;letter-spacing:-3px}.lead{font-size:17px}.hero-art{height:410px}.photo-main{height:350px}.photo-small{width:135px;height:155px}.hello-card{width:110px;height:110px}.hello-card span{font-size:22px}.doodle{display:none}.location-pill{display:none}.section-wrap{width:calc(100% - 40px)}.intro,.support{padding:80px 0}.intro-grid{grid-template-columns:1fr;gap:35px}.intro h2,.section-heading h2{letter-spacing:-2.5px}.support-grid{grid-template-columns:1fr;margin-top:42px}.support-card{min-height:285px}.community{grid-template-columns:1fr}.community-photo{min-height:380px}.community-copy{padding:70px 25px}.final-cta{padding:90px 20px}.final-cta h2{letter-spacing:-2.5px}.actions{flex-wrap:wrap}.centered-actions{flex-direction:column}.footer-row{grid-template-columns:1fr;gap:32px}.footer-links{justify-content:flex-start}.footer-bottom{gap:20px}.footer-bottom span:last-child{text-align:right}}
	@media(prefers-reduced-motion:reduce){:global(html){scroll-behavior:auto}:global(.reveal){opacity:1;transform:none;transition:none}}

	/* Warm KAWAN theme */
	.brand{font-family:'DM Sans',sans-serif;font-weight:700}.brand.inverse small{color:#ead7c7}
	.button{box-shadow:0 10px 25px #b85c4226}
	.hero{background:linear-gradient(105deg,var(--cream) 0 56%,#e5e8e1 56%)}
	.hero:before{border-color:#b85c421c}
	.eyebrow{font-weight:700;letter-spacing:1.7px}.eyebrow.light{color:#f5e9df}
	.hero h1,.section-heading h2,.intro h2,.community h2,.final-cta h2{font-family:'Newsreader',serif;font-weight:500;line-height:1.02;letter-spacing:-2.2px}
	.hero h1 em,h2 em{font-family:inherit}.lead,.support-card p{color:var(--muted)}
	.text-link,.volunteer-link{border-color:#aaa69f}
	.photo-main{box-shadow:0 30px 60px #57483e24}.photo-small{border-color:#e5e8e1}
	.hello-card{background:#e8c7b7}.hello-card span,.photo-note{font-family:'Newsreader',serif}.doodle{color:var(--sage)}.location-pill,.photo-note{background:#fffdfa}
	.intro{color:#fffaf5}.intro h2 em{color:#f1d6c8}
	.support-card.life{background:#e5e8e1}.support-card.grow{background:var(--oat)}.support-card.belong{background:#f1ddd4}
	.card-icon{border-color:#2f312e55;font-family:'Newsreader',serif}.support-card h3{font-size:28px;letter-spacing:-.5px}
	.community{background:var(--sage-dark)}.community-copy h2 em{color:#efd3c5}.community-copy>p:not(.eyebrow){color:#eef0eb}
	.final-cta{background:var(--oat)}.final-cta:before,.final-cta:after{border-color:#b85c421a}
	footer{background:#343733}.footer-row p{color:#d0d0ca}.footer-bottom{color:#aeb0aa}
	@media(max-width:800px){nav{background:#fffdfa}.hero{background:linear-gradient(160deg,var(--cream) 0 58%,#e5e8e1 58%)}.hero h1{letter-spacing:-2px}}

	/* Minimal hero image */
	.hero-art{height:500px}
	.photo-main{inset:0;width:100%;height:100%;border-radius:24px;box-shadow:0 18px 45px #57483e1f}
	.photo-main img{object-position:center}
	@media(max-width:800px){.hero-art{height:360px}.photo-main{height:100%;border-radius:18px}}

	/* Typography-first hero */
	.hero{display:flex;min-height:720px;align-items:center;justify-content:center;padding:130px 24px 90px;text-align:center;background:var(--cream)}
	.hero:before{top:50%;left:50%;width:540px;height:540px;border-color:#b85c4212;transform:translate(-50%,-50%)}
	.hero-copy{display:flex;max-width:850px;flex-direction:column;align-items:center}
	.hero h1{font-size:clamp(58px,8vw,104px);line-height:.94;letter-spacing:-3.5px}
	.lead{max-width:570px;margin:30px auto;font-size:18px}
	@media(max-width:800px){.hero{min-height:650px;padding:120px 22px 75px;background:var(--cream)}.hero:before{width:390px;height:390px}.hero h1{font-size:clamp(52px,15vw,72px);letter-spacing:-2.5px}.hero .actions{justify-content:center}}

	/* Welcoming neutral palette */
	.brand.inverse small{color:#d9e1e4}
	.button{box-shadow:0 10px 25px #63798522}
	.hero:before,.final-cta:before,.final-cta:after{border-color:#63798518}
	.eyebrow.light{color:#e8edef}
	.intro{color:#fff}.intro h2 em{color:#dce5e8}
	.support-card.life{background:#e3eaed}.support-card.grow{background:#ece8e1}.support-card.belong{background:#f1efeb}
	.community{background:#56615d}.community-copy h2 em{color:#dfe7e3}
	footer{background:#30322f}

	/* Fresh, contemporary student palette */
	.brand.inverse small{color:#b9c3ff}
	.hero h1,.section-heading h2,.intro h2,.community h2,.final-cta h2{font-family:'Plus Jakarta Sans',sans-serif;font-weight:700;line-height:1;letter-spacing:-4px}
	.hero h1 em,h2 em{font-family:inherit;font-style:normal;font-weight:700}
	.hero:before,.final-cta:before,.final-cta:after{border-color:#5965d81a}
	.button{border-radius:10px;box-shadow:0 10px 25px #5965d824}
	.eyebrow.light{color:#dfe3ff}
	.intro{background:#5965d8}.intro h2 em{color:#dfe3ff}
	.support-card{border:1px solid #e7e8ed}.support-card.life{background:#e8edff}.support-card.grow{background:#f1f3f8}.support-card.belong{background:#edf4f7}
	.community{background:#293a51}.community-copy h2 em{color:#b8ceef}
	.final-cta{background:#f0f1f5}
	footer{background:#20222a}
	@media(max-width:800px){.hero h1{letter-spacing:-3px}}

	/* Calm, low-saturation finish */
	.brand.inverse small{color:#d4d9dc}
	.hero:before,.final-cta:before,.final-cta:after{border-color:#65717d18}
	.button{box-shadow:0 10px 25px #505b661c}
	.eyebrow.light{color:#e2e6e8}
	.intro{background:#65717d}.intro h2 em{color:#e5e9eb}
	.support-card{border-color:#e5e7e8}.support-card.life{background:#e9edef}.support-card.grow{background:#f1f1ef}.support-card.belong{background:#edf0ef}
	.community{background:#46515b}.community-copy h2 em{color:#dce3e6}
	.final-cta{background:#f0f1f1}
	footer{background:#292d32}

	/* Warm Modern palette */
	.brand.inverse small{color:#d8c4a8}
	.hero{background:#faf8f5}.hero:before,.final-cta:before,.final-cta:after{border-color:#c9785c1f}
	.button{box-shadow:0 10px 25px #365c4a24}.button.gold{color:#2d3748;background:#d8c4a8}
	.eyebrow span{background:#c9785c}.eyebrow.light{color:#f2e9df}
	.intro{background:#365c4a}.intro h2 em{color:#d8c4a8}
	.support-card{border-color:#e7e3dd}.support-card.life{background:#eaf0ec}.support-card.grow{background:#f3ede5}.support-card.belong{background:#f4e5df}
	.community{background:#2d3748}.community-copy h2 em{color:#d8c4a8}
	.final-cta{background:#f3ede5}
	footer{background:#252f3e}

	/* Soft & Welcoming palette */
	.brand.inverse small{color:#e8d9c5}
	.hero{background:#fcfaf7}.hero:before,.final-cta:before,.final-cta:after{border-color:#d79a9a24}
	.button{box-shadow:0 10px 25px #50627a24}.button.gold{color:#303846;background:#e8d9c5}
	.eyebrow span{background:#d79a9a}.eyebrow.light{color:#f2e9e9}
	.intro{background:#50627a}.intro h2 em{color:#e8d9c5}
	.support-card{border-color:#e8e3dc}.support-card.life{background:#e8eee7}.support-card.grow{background:#f5eee5}.support-card.belong{background:#f4e5e3}
	.community{background:#46566a}.community-copy h2 em{color:#e8d9c5}
	.final-cta{background:#f5eee5}
	footer{background:#303846}

	/* Cozy coffee shop palette */
	.brand.inverse small{color:#d9e0d4}
	.hero{background:#fbf8f4}.hero:before,.final-cta:before,.final-cta:after{border-color:#c9866b24}
	.button{box-shadow:0 10px 25px #c9866b26}.button.gold{color:#3d3d3d;background:#a7b49e}
	.eyebrow span{background:#c9866b}.eyebrow.light{color:#f2e8e2}
	.intro{background:#6d5c54}.intro h2 em{color:#e7c1b1}
	.support-card{border-color:#e5ddd6}.support-card.life{background:#e7ece3}.support-card.grow{background:#f1e9e1}.support-card.belong{background:#f1e2dc}
	.community{background:#6d5c54}.community-copy h2 em{color:#dce4d7}
	.final-cta{background:#f1e9e1}
	footer{background:#3d3d3d}

	/* About dropdown and vision/mission */
	.nav-dropdown{position:relative}.nav-dropdown summary{display:flex;align-items:center;gap:7px;cursor:pointer;font-size:14px;font-weight:600;list-style:none}.nav-dropdown summary::-webkit-details-marker{display:none}.nav-dropdown summary span{font-size:13px;transition:transform .2s}.nav-dropdown[open] summary span{transform:rotate(180deg)}
	.dropdown-menu{position:absolute;top:30px;left:-18px;display:grid;width:230px;padding:9px;border:1px solid var(--line);border-radius:12px;background:#fffdf9;box-shadow:0 16px 40px #3d3d3d18}.dropdown-menu a{padding:12px 13px;border-radius:8px}.dropdown-menu a:hover{background:#f3ece6}
	.vision{display:grid;grid-template-columns:.7fr 1.3fr;gap:80px;padding:110px 0}.vision-heading h2{margin:0;font:700 clamp(42px,5vw,64px)/1 'Plus Jakarta Sans',sans-serif;letter-spacing:-3px}.vision-grid{display:grid;grid-template-columns:1fr 1fr;gap:18px}.vision-grid article{padding:36px;border:1px solid var(--line);border-radius:14px;background:#fffdf9}.vision-grid small{color:var(--forest);font-size:10px;font-weight:800;letter-spacing:1.7px}.vision-grid h3{margin:55px 0 15px;font-size:27px;line-height:1.15;letter-spacing:-1px}.vision-grid p{margin:0;color:var(--muted);line-height:1.7}
	@media(max-width:800px){.nav-dropdown{width:100%}.nav-dropdown summary{padding:13px}.dropdown-menu{position:static;width:100%;margin:0;padding:4px 10px;border:0;background:#f7f2ed;box-shadow:none}.dropdown-menu a{padding:11px 12px}.vision{grid-template-columns:1fr;gap:38px;padding:75px 0}.vision-grid{grid-template-columns:1fr}.vision-grid h3{margin-top:36px}}

	/* Typography and component system */
	.brand{font-family:'Inter',sans-serif}
	.hero h1,.section-heading h2,.intro h2,.community h2,.final-cta h2,.vision-heading h2,.support-card h3,.vision-grid h3{font-family:'DM Serif Display',serif;font-weight:400;letter-spacing:-1.5px}
	.hero h1 em,h2 em{font-family:inherit;font-weight:400;font-style:italic}
	.button,.button.gold{border-radius:14px;color:#fff;background:#c9866b;box-shadow:0 8px 22px #c9866b20;transition:background .2s ease,transform .2s ease,box-shadow .2s ease}
	.button:hover,.button.gold:hover{color:#fff;background:#af7059;box-shadow:0 10px 26px #af705926;transform:translateY(-1px)}
	.support-grid,.vision-grid{gap:24px}
	.support-card,.vision-grid article{border:1px solid #eee9e4;border-radius:24px;background:#fff;padding:42px;box-shadow:0 10px 32px rgba(109,92,84,.055)}
	.support-card h3{margin-top:78px;font-size:31px}.vision-grid h3{font-size:30px}
	.dropdown-menu{border-radius:16px;background:#fff;box-shadow:0 12px 35px rgba(109,92,84,.08)}
	@media(max-width:800px){.support-card,.vision-grid article{padding:32px}.hero h1{letter-spacing:-1.5px}}
</style>
