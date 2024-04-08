<script>
  import { Router, Route, Link } from 'svelte-routing';
  import Home from './components/Home.svelte';
  import Sesso from './components/Sesso.svelte';
  import Oggetti from './components/Oggetti.svelte';
  import Eta from './components/Eta.svelte';
</script>

<Router>
  <nav class="navbar">
    <Link to="/">HOME</Link>
    <Link to="/sesso">SESSO</Link>
    <Link to="/oggetti">OGGETTI</Link>
    <Link to="/eta">ETÀ</Link>
  </nav>
  <Route path="/" component={Home} />
  <Route path="/sesso" component={Sesso} />
  <Route path="/oggetti" component={Oggetti} />
  <Route path="/eta" component={Eta} />
</Router>