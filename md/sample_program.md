<!--
    =====================================
    generator=datazen
    version=3.1.4
    hash=ea41b6669ace6999d209f9febe3680e6
    =====================================
-->

# `sample_program.py`

---

    (source below)
    #!/usr/bin/env python
    
    """
    A sample program.
    """
    
    # built-in
    from contextlib import suppress
    import os
    import sys
    import time
    
    
    def main(argv: list[str]) -> int:
        """A sample program entry."""
    
        # CLI arguments not currently used.
        print("arguments: " + ", ".join(argv), flush=True)
    
        # Enable polling read.
        os.set_blocking(sys.stdin.fileno(), False)
    
        keep_going = True
        idx = 0
    
        with suppress(KeyboardInterrupt):
            while keep_going:
                time.sleep(0.5)
    
                print(f"stdout message ({idx})", flush=True)
                print(f"stderr message ({idx})", file=sys.stderr, flush=True)
    
                data = sys.stdin.buffer.read()
                if data is not None:
                    if not data:
                        keep_going = False
                        msg = "got eof - exiting"
                    else:
                        msg = f"got stdin: '{data.decode().rstrip()}'"
    
                    print(msg, flush=True)
                    print(msg, file=sys.stderr, flush=True)
    
                idx += 1
    
        # Use an arbitrary return value.
        return idx % 64
    
    
    if __name__ == "__main__":
        sys.exit(main(sys.argv))

---
