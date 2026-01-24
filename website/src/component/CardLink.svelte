<script lang="ts">
    let {cardTitle, cardLink, cardIcon} = $props();
    import { getIconPath } from '$lib/utils';
</script>

<div class="column is-one-third">
    <a href={cardLink}>
        <figure class="image is-64x64">
            <img src={getIconPath(cardIcon, true)} alt="Icon for {cardTitle}" height="64" width="64">
        </figure>
        <p class="title is-5">{cardTitle}</p>
      </a>
</div>